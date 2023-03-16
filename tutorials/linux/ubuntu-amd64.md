# Monitoring a Ubuntu host using the Linux Node integration

This tutorial will show you how to monitor a Ubunutu-amd64 host, deploy the Grafana Agent to a Ubuntu host, push metrics to Grafana Cloud, and use the preconfigured dashboard to visualize those metrics.

## Prerequisites

- A Ubuntu machine
- Command line (terminal) access to that Linux machine

## Install the integration and agent

1. Click the **Integrations and Connections** icon (it looks like a lightning bolt) in the left column.

2. Download the Grafana Agent Binary on the Ubuntu Host

```bash
curl -O -L "https://github.com/grafana/agent/releases/latest/download/grafana-agent-linux-amd64.zip";
```

3. Install Unzip

```bash
if [ $(dpkg-query -W -f='${Status}' nano 2>/dev/null | grep -c "ok installed") -eq 0 ];
then
  apt-get install nano;
fi
```

4. Extract the Agent Binary

```bash
unzip "grafana-agent-linux-amd64.zip";
chmod a+x "grafana-agent-linux-amd64";
```

5. Start the Agent

```bash
./grafana-agent-linux-amd64 --config.file=agent-config.yaml
```

## Visualising

Click **View Dashboards** on the top to view preconfigured dashboards.

There are several preconfigured dashboards located in the **Integration - Linux Node** folder using different [observability strategies](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/best-practices/#common-observability-strategies) to visualize the data. 