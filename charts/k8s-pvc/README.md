k8s-pvc
=======
A Helm chart for Creating pv/pvc on docker-for-mac

Current chart version is `38.130.3`

Source code can be found [here](https://github.com/georgedriver/helm-charts)

## Installation

### Add Helm repository

```shell
helm repo add georgedriver https://georgedriver.github.io/helm-charts
helm repo update
```

```shell
helm install --generate-name k8s-pvc
```

## Configuration

The following table lists the configurable parameters of the chart and the default values.

## Chart Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| hostPath | string | `"/tmp"` | hostPath that docker for mac used to persistence the data |
| name | string | `"test"` | name for pv/pvc |
| storage | string | `"256Mi"` | storage size for pv/pvc |
| storageClassName | string | `"manual"` | storageClassName for pv/pvc |

## Ref

- [[Kubernetes] Custom Data on Persistant Volume lost on Mac restart](https://github.com/docker/for-mac/issues/4019#issuecomment-575579113)
