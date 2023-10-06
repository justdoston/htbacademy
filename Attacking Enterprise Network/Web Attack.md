# careers.inlanefreight.local
I entered that web application, enumerate. I registered and after registration i noticed url like: http://careers.inlanefreight.local/profile?id=9

I tried to brute force and found IDOR vulnerability.

# dev.inlanefreight.local
I tried to gobuster for enumerate .php files:
```bash
gobuster dir -u http://dev.inlanefreight.local -w /usr/share/wordlists/dirb/common.txt -x .php -t 300
```

## output:
```bash
===============================================================
Gobuster v3.1.0
by OJ Reeves (@TheColonial) & Christian Mehlmauer (@firefart)
===============================================================
[+] Url:                     http://dev.inlanefreight.local
[+] Method:                  GET
[+] Threads:                 300
[+] Wordlist:                /usr/share/wordlists/dirb/common.txt
[+] Negative Status codes:   404
[+] User Agent:              gobuster/3.1.0
[+] Extensions:              php
[+] Timeout:                 10s
===============================================================
2022/06/20 22:04:48 Starting gobuster in directory enumeration mode
===============================================================
/.htaccess            (Status: 403) [Size: 288]
/.htpasswd            (Status: 403) [Size: 288]
/.hta                 (Status: 403) [Size: 288]
/.htpasswd.php        (Status: 403) [Size: 288]
/.hta.php             (Status: 403) [Size: 288]
/css                  (Status: 301) [Size: 332] [--> http://dev.inlanefreight.local/css/]
/images               (Status: 301) [Size: 335] [--> http://dev.inlanefreight.local/images/]
/index.php            (Status: 200) [Size: 2048]                                            
/index.php            (Status: 200) [Size: 2048]                                            
/js                   (Status: 301) [Size: 331] [--> http://dev.inlanefreight.local/js/]    
/server-status        (Status: 403) [Size: 288]                                             
/uploads              (Status: 301) [Size: 336] [--> http://dev.inlanefreight.local/uploads/]
/upload.php           (Status: 200) [Size: 14]                                               
/.htaccess.php        (Status: 403) [Size: 288]                                              
                                                                                             
===============================================================
2022/06/20 22:05:02 Finished
===============================================================
```
