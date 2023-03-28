# Send metrics, logs and traces to Grafana Cloud from self-hosted Prometheus, Loki and Tempo

## Send metrics to Grafana Cloud from self hosted Prometheus in Kubernetes

To get Prometheus metrics into Grafana Cloud, configure Prometheus to push scraped samples using remote_write. remote_write allows you to forward scraped samples to compatible remote storage endpoints as shown in the following diagram.

![remote write architecture](https://grafana.com/static/img/docs/grafana-cloud/arch_diagrams/localprom.jpg)

## Sending metrics from a single prometheus instance

Add the following remote_write snippet to your Prometheus configuration file (often prometheus.yml). You can find the /api/prom/push URL, username, and password for your metrics endpoint by clicking on Details in the Prometheus card of the Cloud Portal:

```yaml
remote_write:
- url: <Your Metrics instance remote_write endpoint>
  basic_auth:
    username: <Your Metrics instance ID>
    password: <Your Grafana.com API Key>
```

If you are using the Prometheus Helm chart, You can add the above configuration under the remote_write variable in [values.yml](https://github.com/prometheus-community/helm-charts/blob/main/charts/prometheus/values.yaml) and run

```bash
helm update [RELEASE_NAME] -f values.yml
```

## Sending metrics from multiple prometheus instance

When sending metrics from multiple Prometheus instances, you can use the external_labels parameter to label time series data with an instance identifier. Append any external_labels to the global section of your Prometheus configuration file. You can find the /api/prom/push URL, username, and password for your metrics endpoint by clicking on Details in the Prometheus card of the Cloud Portal:

First Prometheus instance:

```yaml
global:
  external_labels:
    origin_prometheus: prometheus01
remote_write:
- url: <Your Metrics instance remote_write endpoint>
  basic_auth:
    username: <Your Metrics instance ID>
    password: <Your Grafana.com API Key>
```

Second Prometheus instance:

```yaml
global:
  external_labels:
    origin_prometheus: prometheus02
remote_write:
- url: <Your Metrics instance remote_write endpoint>
  basic_auth:
    username: <Your Metrics instance ID>
    password: <Your Grafana.com API Key>
```

If you are using the Prometheus Helm chart, You can add the above configuration under the `global` and `remote_write` variable in [values.yml](https://github.com/prometheus-community/helm-charts/blob/main/charts/prometheus/values.yaml) and run

```bash
helm update [RELEASE_NAME] -f values.yml
```

## Sending metrics from multiple high-availability Prometheus instances

If you’re shipping data to Grafana Cloud Metrics from multiple Prometheus instances in a high-availability (HA) configuration, you should use the cluster and __replica__ labels to deduplicate data received at the Grafana Cloud Metrics endpoint. Add these to the external_labels section in your Prometheus configuration file. You can find the /api/prom/push URL, username, and password for your metrics endpoint by clicking on Details in the Prometheus card of the Cloud Portal:

First HA Prometheus instance:

```yaml
global:
  external_labels:
    cluster: prom-team1
    __replica__: replica1
remote_write:
- url: <Your Metrics instance remote_write endpoint>
  basic_auth:
    username: <Your Metrics instance ID>
    password: <Your Grafana.com API Key>
```

Second HA Prometheus instance:

```yaml
global:
  external_labels:
    cluster: prom-team1
    __replica__: replica2
remote_write:
- url: <Your Metrics instance remote_write endpoint>
  basic_auth:
    username: <Your Metrics instance ID>
    password: <Your Grafana.com API Key>
```

If you are using the Prometheus Helm chart, You can add the above configuration under the `global` and `remote_write` variable in [values.yml](https://github.com/prometheus-community/helm-charts/blob/main/charts/prometheus/values.yaml) and run

```bash
helm update [RELEASE_NAME] -f values.yml
```

The cluster label will identify the HA Prometheus cluster shipping data to Grafana Cloud Metrics. The __replica__ label should be set to a unique value within the HA Prometheus cluster. It will be dropped when Grafana Cloud Metrics deduplicates and ingests the data.