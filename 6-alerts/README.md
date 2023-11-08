# Connector

1. Goto Kibana > Stack Management > Connectors
2. Create Connector > Index
3. Connector name : student alerts
4. Write to index : logs-student-alerts

# Alerts

1. Go to Kibana > Security > Rules > Detection rules (SIEM)
2. Create New Rule
3. Step 1 config:
   * Custom Query
   * Index patterns : filebeat-* logs-*
   * Custom Query : `data_stream.dataset : "system.auth" and user.name : ubuntu`
   * Timeline Template : "Generic Match Timeline"
   * Tags : student
4. Step 2 config:
   * name : student rule
5. Step 3 config:
   * schedule : 1 minute
6. Step 4 config:
   * Index : student index
   * Action Frequency : For each alert : Per rule run
   * Document to index :
```json
{
"rule_id": "{{rule.id}}",
"rule_name": "{{rule.name}}",
"alert_id": "{{alert.id}}",
"context_message": "{{context.message}}"
}
```

## Add an exception
1. Go to Security > Rules > Detection rules (SIEM)
2. search for `student` rule
3. Rule Exceptions
4. name : student
5. field : source.ip is `3.67.188.184`
6. Check "Close all alerts that match this exception"

## Shared exceptions
1. Go to Security > Rules > Shared exceptions
2. Create shared exception list : student
3. Add exception to list : "Lab ip"
4. source.ip is 3.67.188.184
5. Link rules : student rule