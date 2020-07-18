k8s-alert-receiver
==================
A Helm creates k8s CR for alertmanager recevier (using alert-operator) on k8s

Current chart version is `0.0.1`

Source code can be found [here](https://github.com/georgedriver/helm-charts)

## Installation

### Add Helm repository

```shell
helm repo add georgedriver https://georgedriver.github.io/helm-charts
helm repo update
```

```shell
helm install --generate-name alert-operator
```


## Chart Content
The chart will create a CR with 2 receivers (based on the provided values):
1. Slack receiver (if slace webhook_url was provided).
2. pagerduty receiver (if pagerduty service_key was provided)

## k8s-alert-receiver Configuration
The following values are set in this chart values.yaml, some overwrite the sub-chart values

## Configuration

The following table lists the configurable parameters of the chart and the default values.

## Chart Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| enable_default_router | bool | `true` |  |
| pagerduty.name | string | `""` |  |
| pagerduty.service_key | string | `""` |  |
| slack.channel | string | `""` |  |
| slack.name | string | `"null"` |  |
| slack.webhook_url | string | `""` |  |
| target_configuration.name | string | `"alertmanager"` |  |
| target_configuration.namespace | string | `"system-monitoring"` |  |

## Monitoring

### Service Monitor Resource
When monitoring enabled, a ServiceMonitor will be created to auto-add the alert-operator metrics to Prometheus. Check the Prometheus Operator Service Monitor for details.

## Grafana Dashaboard
When monitoring enabled, Helm will create a config map resources with the label of "grafana-dashboard" to store alert-operator dashboards.
If you want to add a new dashboard, create the dashboard, export it to a JSON file and put it in the "dashboards" folder under the charts.
Grafana will auto-detect any dashboard based on the label, and load it.

## Prometheus Rules
PrometheusRules resource is used to create Prometheus alerts. If alerting enabled, helm will create the resource for Prometheus to auto-detect it.
To create/modify alerts - edit the PrometheusRules resource file in the templates folder and change the spec. See Prometheus documantation for more details on alerts.

## Alert Manager
AlertManager resource will handle spinning a new instance of alertmanager for your application.
Use alert manager resource, and it's Configuration to set how your alerts are being handled - if you want to push them to Pagerduty/email/slack etc.
See Prometheus Alert Manager documantation for more details
