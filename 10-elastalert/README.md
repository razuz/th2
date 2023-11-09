# Elastalert

### Elastic
1. Go to your Kibana
2. Stack Management > Roles
3. Create Role `elastalert_role` and give it :
    - cluster privileges : monitor, manage_index_templates
    - Index privileges `read`, `write`, `auto_configure`, `create_index`, `manage` for indices `elastalert`, `elastalert_status`, `elastalert_error`, `past_elastalert`, `elastalert_silence`
    - Index privileges `read` for indices `.alerts-security*`
4. Go to your Kibana > Stack Management > Users > Create User
5. Add new user `elastalert` and attach role `elastalert_role`

### Elastalert

1. Get API key for TheHive
2. SSH into the jumphost
```shell
ssh studentX@lab.threatlab.ninja
```
3. update your git repo folder th2
```shell
cd th2/
git pull
```
4. Go to `10-elastalert` folder and update helm chart dependencies
```shell
cd 10-elastalert/elastalert2
helm dependency build
```
5. update `values.yaml` according to your parameters
   * replace studentX with your student number
   * update password for `elastalert` user
   * add Hive API key : `hp5VaEXUV4bgMbLCJVhcvHqwhrVTXD8E` 
6. Run Elastalert
```shell
helm upgrade elastalert ./elastalert2/ --create-namespace --install -n studentX
```
7. Go to Kibana > Dev Tools and run the following command to fix index
```json
PUT /elastalert/_mapping
{
  "properties": {
      "alert_time": {"type": "date"}
  }
}
```