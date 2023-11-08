# Detection Tasks

## Enable powershell script block logging
```
New-Item -Path "HKLM:\SOFTWARE\Wow6432Node\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Force
Set-ItemProperty -Path "HKLM:\SOFTWARE\Wow6432Node\Policies\Microsoft\Windows\PowerShell\ScriptBlockLogging" -Name "EnableScriptBlockLogging" -Value 1 -Force
```

## Task 1
Create a query and alert for scheduled task creation on Windows.

## Task 2
Create a query for renamed PE and the value of process.pe.* fields

## Task 3
What's wrong with the rule : Account Discovery Command via SYSTEM Account

## Task 4
Create a query and alert for certutil file downloads

## Task 5
Create a query and alert for failed SSH logins on your linux host