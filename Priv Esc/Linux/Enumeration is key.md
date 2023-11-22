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
**All Hidden Files:** `find / -type f -name ".*" -exec ls -l {} \; 2>/dev/null`<br>
**All Hidden Directories:** `find / -type d -name ".*" -ls 2>/dev/null`<br>
**Finding History Files:** `find / -type f \( -name *_hist -o -name *_history \) -exec ls -l {} \; 2>/dev/null`<br>
**Configuration Files:** `find / -type f \( -name *.conf -o -name *.config \) -exec ls -l {} \; 2>/dev/null`<br>
**Scripts:** `find / -type f -name "*.sh" 2>/dev/null | grep -v "src\|snap\|share"`<br>

## System and Services

**Cronjobs:**
```bash
cat /etc/crontab
ls -la /etc/cron.daily
```
**Proc file system**
The proc filesystem (proc / procfs) is a particular filesystem in Linux that contains information about system processes, hardware, and other system information. 
```bash
find /proc -name cmdline -exec cat {} \; 2>/dev/null | tr " " "\n"
```
**Installed packages:**
```bash
apt list --installed | tr "/" " " | cut -d" " -f1,3 | sed 's/[0-9]://g' | tee -a installed_pkgs.list
```
**Binaries:**
```bash
ls -l /bin /usr/bin/ /usr/sbin/
```
**Trace System Calls**
The output of strace can be written to a file for later analysis, and it provides a wealth of options that allow detailed monitoring of the program's behavior.
```bash
strace ping -c 1 192.168.X.X
```




