# The Hive & Cortex

Elastic & Cassandra both need increased vm.max_map_count so on the host machine need to do:

```
sysctl -w vm.max_map_count=1048575
```
