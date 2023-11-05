# installing elastic

## Deployment
1. eck-operator
```shell
helm upgrade eck-operator ./charts/eck-operator/ -n studentX --create-namespace --install
```
2. eck-elasticsearch
```shell
helm upgrade eck-elasticsearch ./charts/eck-elasticsearch/ -n studentX --create-namespace --install`
```
3. eck-kibana
```shell
helm upgrade eck-kibana ./charts/eck-kibana/ -n studentX --create-namespace --install`
```
4. eck-fleet (in case you want to use fleet)
```shell
helm upgrade eck-fleet ./charts/eck-fleet/ -n studentX --create-namespace --install`
```
