alert-operator
==============
A k8s prometheus alert-operator chart

Current chart version is `0.0.2`

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
The chart will provide the following resources:
1. Alert Operator CRD's resource (installed first using helm CRD hook)
2. Alert operator supporting service-account, cluster-role and cluster-role-binding resources.
3. Alert-operator deployment
4. Alert-operator service,  ServiceMonitor & monitoring resources. *** currently disabled by default as prometheus metrics are not yet supported ***

## Configuration

The following table lists the configurable parameters of the chart and the default values.

## Chart Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| affinity | object | `{}` |  |
| fullnameOverride | string | `""` |  |
| image.pullPolicy | string | `"Always"` |  |
| image.repository | string | `"georgedriver/alert-operator"` |  |
| image.tag | string | `"master"` |  |
| monitoring.alerting.enable | bool | `false` |  |
| monitoring.enabled | bool | `false` |  |
| nameOverride | string | `""` |  |
| nodeSelector | object | `{}` |  |
| replicaCount | int | `1` |  |
| resources | object | `{}` |  |
| service.port | int | `60000` |  |
| tolerations | list | `[]` |  |

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
