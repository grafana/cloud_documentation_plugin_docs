# Monitoring a Debian host using the Linux Node integration

This tutorial will show you how to monitor a Debian-amd64 host, deploy the Grafana Agent to a Ubuntu host, push metrics to Grafana Cloud, and use the preconfigured dashboard to visualize those metrics.

## Prerequisites

- A Debian machine
- Command line (terminal) access to that Linux machine

## Install the integration and agent

1. Click the **Integrations and Connections** icon (it looks like a lightning bolt) in the left column.

2. Download the Grafana Agent Binary on the Debian Host

```bash
sudo ARCH="amd64" GCLOUD_STACK_ID="560581" GCLOUD_API_KEY="eyJrIjoiZjViYWYyMDgzZGY4MzE5NWNhZDI2MDFhMWQwZjNmODllM2Q1NGZlMyIsIm4iOiJzdGFjay01NjA1ODQtZWFzeXN0YXJ0LWdjb20iLCJCI6NjUyOTkyfQ==" GCLOUD_API_URL="https://integrations-api-us-central.grafana.net" /bin/sh -c "$(curl -fsSL https://raw.githubusercontent.com/grafana/agent/release/production/grafanacloud-install.sh)"
```

3. Start the Agent

```bash
sudo systemctl restart grafana-agent.service
```

## Visualising

Click **View Dashboards** on the top to view preconfigured dashboards.

There are several preconfigured dashboards located in the **Integration - Linux Node** folder using different [observability strategies](https://grafana.com/docs/grafana/latest/dashboards/build-dashboards/best-practices/#common-observability-strategies) to visualize the data. 