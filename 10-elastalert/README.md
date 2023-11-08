# Elastalert

### Elastic
1. Go to your Kibana
2. Stack Management > Roles
3. Create Role `elastalert_role` and give it :
    - cluster privileges : monitor, manage_index_templates
    - Index privileges `all` for indices `elastalert`
4. Go to your Kibana > Stack Management > Users > Create User
5. Add new user `elastalert` and attach role `elastalert_role`

