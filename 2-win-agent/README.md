# Elastic agent

1. Log into your windows VM (Both RDP & SSH are available)
2. Open a PowerShell window as admin
3. Install sysmon on the host with:

   ```

   Invoke-WebRequest -Uri "https://raw.githubusercontent.com/olafhartong/sysmon-modular/master/sysmonconfig-excludes-only.xml" -OutFile "C:\Users\student\Downloads\config.xml"
   Invoke-WebRequest -Uri "https://live.sysinternals.com/Sysmon64.exe" -OutFile "C:\Users\student\Downloads\Sysmon64.exe"
   C:\Users\student\Downloads\Sysmon64.exe -accepteula -i C:\Users\student\Downloads\config.xml
   ```

   > [!NOTE]
   > This sysmon config only has exclude statements. This means it's quite heavy in log volume. Think carefully before running that in production

4. Go to Fleet in Kibana
5. On the top right, click the `Add agent` button
6. In the prompt select the `Create new agent policy` option
7. Name the new policy `Windows` and click the `Create policy` button
8. Leave step 2 as the default of enrolling to Fleet
9 In step 3 click the tab titled Windows and run the provided PowerShell code in the Windows VM from an admin terminal
10. You should then see an agent check in and data start flowing
