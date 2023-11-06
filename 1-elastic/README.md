# installing elastic

# getting the sources

```shell
git clone https://github.com/razuz/th2.git
```

## Deployment

1. eck-operator

```shell
helm upgrade eck-operator ./charts/eck-operator/ -n studentX --create-namespace --install
```

2. eck-elasticsearch

```shell
helm upgrade eck-elasticsearch ./charts/eck-elasticsearch/ -n studentX --create-namespace --install
```

3. eck-kibana

```shell
helm upgrade eck-kibana ./charts/eck-kibana/ -n studentX --create-namespace --install
```

4. eck-fleet (in case you want to use fleet)

```shell
helm upgrade eck-fleet ./charts/eck-fleet/ -n studentX --create-namespace --install
```

### Useful commands

* Get elastic password from kubernetes secrets
```
kubectl get secret eck-elasticsearch-es-elastic-user -n studentX -o=jsonpath='{.data.elastic}' | base64 --decode; echo
```
* Get Elasticsearch status from CLI
```shell
kubectl get elasticsearch -n studentX
```
* Show resources in namespace
```shell
kubectl get all -n studentX
```
* Show logs from pod
```shell
kubectl logs -n studentX <pod-name>
```
