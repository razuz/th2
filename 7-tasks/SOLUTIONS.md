# Detection Tasks

## Task 1
Create a query and alert for scheduled task creation on Windows.

event.dataset : "windows.sysmon_operational" and event.category : "process" and event.code : 1 and process.name : "schtasks.exe"

## Task 2
Create a query for renamed PE and the value of process.pe.* fields

event.dataset : "windows.sysmon_operational" and event.category : "process" and event.code : 1 and process.pe.original_file_name : "net1.exe"

## Task 3
What's wrong with the rule : Account Discovery Command via SYSTEM Account

Following process tree is not really useful: 
process.name : "net1.exe" and not process.parent.name : "net.exe"

## Task 4
Create a query and alert for certutil file downloads

```jsx
sequence with maxspan = 15m
      [ process where process.name == "certutil.exe"]
      [ network where network.protocol in ("http", "https") and user_agent.original == "CertUtil URL Agent"]
```
or:
event.code : "1" and process.name : "certutil.exe" and process.args : http*

## Task 5
Create a query and alert for failed SSH logins on your linux host

host.name : "student5linux" and event.dataset : "system.auth" and event.outcome : "failure" 