# Elastic Agent for Linux

## install agent
1. Goto Kibana Fleet > Agent Policies
2. Create Agent Policy "Linux"
3. Goto Kibana Fleet > Agents 
   1. Click "Add Agent"
   2. Choose policy "Linux"
   3. Copy the command to clipboard from "Step 3: Install Agent on your host"
4. Log into your Linux VM via SSH 
```shell
ssh studentX@studentX.ec2.threatlab.ninja
```
5. Paste the command from the clipboard and run it
6. You should then see an agent check in on Kibana and data start flowing

## install integrations
1. Goto Kibana Integrations
2. Search for "linux"
3. Add "Audit Logs"
4. Add the integration to "Existing Hosts" and choose Agent Policy "Linux"
5. Save and Deploy
