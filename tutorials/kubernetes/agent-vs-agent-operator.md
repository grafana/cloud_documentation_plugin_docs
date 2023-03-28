## Grafana Agent versus Grafana Agent Operator

The Kubernetes Monitoring interface lets you choose between Grafana Agent and Grafana Agent Operator to set up Kubernetes Monitoring. The following sections describe them to help you decide.

### Grafana Agent

Grafana Agent collects and forwards telemetry data (metrics, logs and traces) to Grafana deployments&mdash; Grafana Open Source, Grafana Cloud, or Grafana Enterprise. Kubernetes Monitoring uses Grafana Agent to ship the telemetry data to Grafana Cloud.

### Grafana Agent Operator

Grafana Agent Operator is a [Kubernetes operator](https://kubernetes.io/docs/concepts/extend-kubernetes/operator/) that makes it easier to deploy Grafana Agent to collect telemetry data from your pods.

Grafana Agent Operator is an abstraction over Grafana Agent. Agent Operator ultimately makes it easier to configure and run in Kubernetes clusters.

Grafana Agent Operator watches Kubernetes custom resources that specify:

- How to collect telemetry data from your Kubernetes cluster
- Where to send the telemetry data

If you choose Agent Operator, you're actually using Grafana Agent beneath to collect and send telemetry data from your Kubernetes cluster.

Grafana Agent Operator deploys custom resources for MetricsInstance, LogsInstance, PodLogs, and others. It helps distribute the configuration for metrics and logs unlike Grafana Agent, which relies on a single large config map.

Grafana Agent Operator also makes scaling easier. It manages your deployments of Grafana Agent for you. If you run Grafana Agent directly in Kubernetes, you need to manage the deployments manually.

The following table compares Grafana Agent and Grafana Agent Operator.

| Property                 | Grafana Agent | Grafana Agent Operator |
| :----------------------- | :-----------: | :--------------------: |
| Kubernetes native        |   &#x2718;    |        &#x2713;        |
| Helm Chart               |   &#x2713;    |        &#x2713;        |
| Works outside Kubernetes |   &#x2713;    |        &#x2718;        |

For details, see the [Grafana Agent](https://grafana.com/docs/agent/latest/) and [Grafana Agent Operator](https://grafana.com/docs/agent/latest/operator/) documentation.
