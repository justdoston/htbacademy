# First of all enumeration !

**OS Version**`uname -a` and `cat /etc/os-release`<br>
**Kernel Version** `uname -r`<br>
**Running Services**<br>
**Linux current process:**
```bash
ps aux | grep root
```
**Full basic system info**
```bash
hostnamectl and neofetch
```
**Host info** `lscpu`<br>
**Installed Packages and Versions**
**Logged in users:**
```bash
ps au
w
```
**Bash history** `history`

# Enumeration permission based

**Sudo privilege:** `sudo -l`<br>
**Suid bit set:** `find / -user root -perm -4000 -exec ls -ldb {} \; 2>/dev/null`<br>
**Setguid bit set:** `find / -user root -perm -6000 -exec ls -ldb {} \; 2>/dev/null`<br>
**Capabilities:** `find /usr/bin /usr/sbin /usr/local/bin /usr/local/sbin -type f -exec getcap {} \;`<br>
**Writable Directories:** `find / -path /proc -prune -o -type d -perm -o+w 2>/dev/null`<br>
**Writable Files:** `find / -path /proc -prune -o -type f -perm -o+w 2>/dev/null`<br>




