# OSQuery

## Install integration

1. Go to Kibana > OSQuery and "Add Osquery Manager"
2. Add the integration to following policies:
    - `Fleet Server on ECK Policy`
    - `Windows`
    - `Linux`
3. Go to Kibana > Integrations > search osquery
4. Add Osquery Logs to the following policies:
    - `Windows`
    - `Linux`

## Enable Query Packs

1. Got to Kibana > OSQuery > Packs
2. Click on "Add Query Packs"
3. Enable all packs except:
    - `osx-attacks`
    - `vuln-management`

## Running queries

1. Go to Kibana > OSQuery > Live Queries
2. New Live Query
3. Single Query
4. Select Agents to target (Linux for example)
5. Find query you'd like to execute
6. Submit
