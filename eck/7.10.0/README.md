# ECK Stack

## Install ECK Operator

```bash
VERSION=2.14.0
kubectl create -f https://download.elastic.co/downloads/eck/$VERSION/crds.yaml
kubectl apply -f https://download.elastic.co/downloads/eck/$VERSION/operator.yaml
```

## Install ECK

```bash
kubectl apply -f manifests.yaml
```

## Setup Fluent Bit

```bash
helm repo add fluent https://fluent.github.io/helm-charts
helm repo update
helm upgrade --install fluent-bit fluent/fluent-bit -f fluentbit-override.yaml
```

## Access Kibana

Port forward the Kibana, acess the UI from `https://localhost:5601/`.

```bash
kubectl port-forward service/quickstart-kb-http 5601
```

The username is `elastic`, and password can be retrieved from the following command.

```bash
kubectl get secret quickstart-es-elastic-user -o=jsonpath='{.data.elastic}' | base64 --decode; echo
```
