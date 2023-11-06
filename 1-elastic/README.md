# installing elastic

# getting the sources

```shell
git clone https://github.com/razuz/th2.git
```

## Deployment

1. eck-operator (SKIP THIS STEP !)

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

### Step 2

Make ingest node publicly accessible.

1. SSH into the jumphost
```shell
ssh studentX@lab.threatlab.ninja
```
2. make changes to your eck-elasticsearch Helm Chart `values.yaml` file
```shell
cd th2/1-elastic/charts/eck-elasticsearch
```
3. remove the following lines:
```yaml
ingress:
  enabled: false
```
and comment in the ingress configuration:
NB! bare in mind the `studentX` placement here !
```shell
ingress:
  enabled: true
  annotations:
    kubernetes.io/ingress.class: alb
    alb.ingress.kubernetes.io/scheme: internet-facing
    alb.ingress.kubernetes.io/target-type: ip
    alb.ingress.kubernetes.io/target-node-labels: 'elasticsearch.k8s.elastic.co/node-ingest=true'
    alb.ingress.kubernetes.io/manage-backend-security-group-rules: "true"
    alb.ingress.kubernetes.io/listen-ports: '[{"HTTP": 80}, {"HTTPS": 443}]'
    alb.ingress.kubernetes.io/ssl-redirect: '443'
    alb.ingress.kubernetes.io/backend-protocol: HTTPS
    alb.ingress.kubernetes.io/load-balancer-name: eck-ingest-studentX
    alb.ingress.kubernetes.io/healthcheck-path: /
    alb.ingress.kubernetes.io/load-balancer-attributes: routing.http.preserve_host_header.enabled=true
    external-dns.alpha.kubernetes.io/hostname: ingest-studentX.threatlab.ninja
  hosts:
    - host: ingest-studentX.threatlab.ninja
      paths:
        - path: /
          pathType: Prefix
          backend:
            service:
              name: eck-elasticsearch-es-ingest
              port:
                number: 9200
```
4. Deploy the eck-elasticsearch Helm Chart again
```shell
cd /home/studentX/th2/1-elastic
```
or
```shell
cd ../..
```
and deploy the chart again
```shell
helm upgrade eck-elasticsearch ./charts/eck-elasticsearch/ -n studentX --create-namespace --install
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
