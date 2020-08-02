# docker-fluentd-ds-cloudlogging

To forward to GCP Cloud Logging as a Daemonset. It's inspired to [fluent/fluentd-kubernetes-daemonset](https://github.com/fluent/fluentd-kubernetes-daemonset)

[![Docker Stars](https://img.shields.io/docker/stars/hiiiide/fluentd-ds-cloudlogging.svg)](https://hub.docker.com/r/hiiiide/fluentd-ds-cloudlogging)
[![Docker Pulls](https://img.shields.io/docker/pulls/hiiiide/fluentd-ds-cloudlogging.svg)](https://hub.docker.com/r/hiiiide/fluentd-ds-cloudlogging)



## Supported tags and respective `Dockerfile` links

See also dockerhub tags page: https://hub.docker.com/r/hiiiide/fluentd-ds-cloudlogging/tags

## How to installation to K8S

### 1. Configure Agent permissions

```
kubectl apply -f https://raw.githubusercontent.com/hiiiide/docker-fluentd-ds-cloudlogging/master/manifests/rbac.yaml
```

### 2. Create Secret

This secret is used in the manifest to deploy the Fluentd.

```yaml
apiVersion: v1
kind: Secret
metadata:
  name: fluentd-secret
  namespace: kube-system
type: Opaque
data:
  foward-host: <ENCODED_BASE64_FOWARD_HOST>
  foward-port: <ENCODED_BASE64_FOWARD_PORT>
  gcp-project-id: <ENCODED_BASE64_GCP_PROJECT_ID>
  gcp-credentials: <ENCODED_BASE64_GCP_CREDENTIALS>
```

### 3. Apply Fluentd config

Please prepare a ConfigMap yourself. I create a sample for your help.

https://gist.github.com/hiiiide/81cde8544b713f72859e25283c25ee6a

### 4. Apply DaemonSet

```
kubectl apply -f https://raw.githubusercontent.com/hiiiide/docker-fluentd-ds-cloudlogging/master/manifests/daemonset.yaml
```

## Image versions

- `0.0.1`, `v0.0.1`, `latest`
  - fluentd: 1.7.4
  - fluent-plugin-google-cloud: 0.8.5
