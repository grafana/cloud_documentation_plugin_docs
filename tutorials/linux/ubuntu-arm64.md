# Monitoring a Ubuntu host using the Linux Node integration

This tutorial will show you how to monitor a Ubunutu-arm64 host, deploy the Grafana Agent to a Ubuntu host, push metrics to Grafana Cloud, and use the preconfigured dashboard to visualize those metrics.

## Prerequisites

- Ubuntu machine
- Command line (terminal) access to that Linux machine

## Install the integration and agent

1. Click the **Integrations and Connections** icon (it looks like a lightning bolt) in the left column.

2. Download the Grafana Agent Binary on the Ubuntu Host

```bash
curl -O -L "https://github.com/grafana/agent/releases/latest/download/grafana-agent-linux-arm64.zip";
```

3. Install Unzip

```bash
if [ $(dpkg-query -W -f='${Status}' unzip 2>/dev/null | grep -c "ok installed") -eq 0 ];
then
  apt-get install unzip;
fi
```

4. Extract the Agent Binary

```bash
unzip "grafana-agent-linux-arm64.zip";
chmod a+x "grafana-agent-linux-amd64";
```

5. Setup Agent Binary
```bash
cat <<EOF > ./agent-config.yaml
integrations:
  node_exporter:
    enabled: true
    relabel_configs:
      - replacement: hostname
        target_label: instance
  prometheus_remote_write:
    - basic_auth:
        password: <your-api-key>
        username: <your-user-id>
      url: https://prometheus-[your-instance-id].grafana.net/api/prom/push
logs:
  configs:
    - clients:
        - basic_auth:
            password: <your-api-key>
            username: <your-user-id>
          url: https://logs-[your-instance-id].grafana.net/loki/api/v1/push
      name: integrations
      positions:
        filename: /tmp/positions.yaml
      scrape_configs:
        - job_name: integrations/node_exporter_journal_scrape
          journal:
            labels:
              instance: hostname
              job: integrations/node_exporter
            max_age: 24h
          relabel_configs:
            - source_labels:
                - __journal__systemd_unit
              target_label: unit
            - source_labels:
                - __journal__boot_id
              target_label: boot_id
            - source_labels:
                - __journal__transport
              target_label: transport
            - source_labels:
                - __journal_priority_keyword
              target_label: level
        - job_name: integrations/node_exporter_direct_scrape
          static_configs:
            - labels:
                __path__: /var/log/{syslog,messages,*.log}
                instance: hostname
                job: integrations/node_exporter
              targets:
                - localhost
      target_config:
        sync_period: 10s
metrics:
  configs:
    - name: integrations
      remote_write:
        - basic_auth:
            password: <your-api-key>
            username: <your-user-id>
          url: https://prometheus-[your-instance-id].grafana.net/api/prom/push
  global:
    scrape_interval: 60s
  wal_directory: /tmp/grafana-agent-wal
EOF
```

6. Start the Agent

```bash
./grafana-agent-linux-amd64 --config.file=agent-config.yaml
```

## Visualising

Click **View Dashboards** on the top to view preconfigured dashboards.

There are several preconfigured dashboards located in the **Integration - Linux Node** folder using different [observability strategies](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/best-practices/#common-observability-strategies) to visualize the data. 
