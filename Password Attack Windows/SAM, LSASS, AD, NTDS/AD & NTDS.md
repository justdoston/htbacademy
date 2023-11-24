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
