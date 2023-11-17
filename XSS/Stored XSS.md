We can start the server below to view and practice a Stored XSS example. As we can see, the web page is a simple To-Do List app that we can add items to. We can try typing test and hitting enter/return to add a new item and see how the page handles it:

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/90c89f11-3e6e-4a1b-9bf0-dea409103442)

## XSS Testing Payloads
We can test it following basic payload:
```bash
<script>alert("Hello World")</script>
```

https://github.com/offensivecyber03/htbacademy/assets/71892943/dde47961-4c15-48f3-9191-bc17dcfeb221

