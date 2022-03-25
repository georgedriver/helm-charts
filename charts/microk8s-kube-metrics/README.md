# microk8s-kube-metrics

A Helm chart for Microk8s controller-manager, scheduler and kube-proxy metrics in Prometheus

## Source Code

* <https://github.com/georgedriver/helm-charts>

## Installation

### Add Helm repository

```shell
helm repo add georgedriver https://georgedriver.github.io/helm-charts
helm repo update
```

```shell
helm install --generate-name microk8s-kube-metrics
```

## Configuration

The following table lists the configurable parameters of the chart and the default values.

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| masterIP | string | `"test"` |  |

`docker run --rm --volume "$(pwd):/helm-docs" -u $(id -u) jnorwood/helm-docs:latest`
