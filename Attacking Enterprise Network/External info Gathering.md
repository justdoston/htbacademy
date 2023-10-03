# Nmap Scan

After using agrressive scan with **-A** flag we can use conveinent output

```bash
sudo nmap --open -p- -A -oA inlanefreight_ept_tcp_all_svc -iL scope
```

The first thing we can see is that this is an Ubuntu host running an HTTP proxy of some kind. We can use this handy Nmap grep cheatsheet to "cut through the noise" and extract the most useful information from the scan. Let's pull out the running services and service numbers, so we have them handy for further investigation.

```bash
egrep -v "^#|Status: Up" inlanefreight_ept_tcp_all_svc.gnmap | cut -d ' ' -f4- | tr ',' '\n' | \                                                               
sed -e 's/^[ \t]*//' | awk -F '/' '{print $7}' | grep -v "^$" | sort | uniq -c \
| sort -k 1 -nr
```

# Performing zone transfer

```bash
dig axfr domain.com @IP
```
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/9e6aa58b-a684-459a-b41f-63827143a010)


# Banner grap scan in nmap

Default script for banner grap scan:

```bash
sudo nmap -sS inlanefreight.local --script=banner
```
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/7d88cc34-4cc0-42cc-ba28-fe57b37deb9c)

Port 53 has no banner so i decided to scan separately:

```bash
sudo nmap -sS inlanefreight.local -sC -sV -p53
```
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/6500f798-8d26-4539-a733-d003679f9a45)

# Host enumeration
Before host enumeration we have to know what response siz will be if wrong:

```bashcurl -s -I http://10.129.203.114 -H "HOST: defnotvalid.inlanefreight.local" | grep "Content-Length:"
Content-Length: 15157
```
15157 is response size for non-existing hosts.

```bash
ffuf -w subdomains-top1million-110000.txt:FUZZ -u http://inlanefreight.local -H 'Host:FUZZ.inlanefreight.local' -fs 15157
```

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/5a6ac996-8c11-47b2-a64c-da5bb4e0b146)


