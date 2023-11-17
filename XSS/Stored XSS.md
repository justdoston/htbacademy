We can start the server below to view and practice a Stored XSS example. As we can see, the web page is a simple To-Do List app that we can add items to. We can try typing test and hitting enter/return to add a new item and see how the page handles it:

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/90c89f11-3e6e-4a1b-9bf0-dea409103442)

## XSS Testing Payloads
We can test it following basic payload:
```bash
<script>alert("Hello World")</script>
```

https://github.com/offensivecyber03/htbacademy/assets/71892943/dde47961-4c15-48f3-9191-bc17dcfeb221

As we can see, we did indeed get the alert, which means that the page is vulnerable to XSS, since our payload executed successfully

```
Tip: Many modern web applications utilize cross-domain IFrames to handle user input, so that even if the web form is vulnerable to XSS, it would not be a vulnerability on the main web application. This is why we are showing the value of window.origin in the alert box, instead of a static value like 1. In this case, the alert box would reveal the URL it is being executed on, and will confirm which form is the vulnerable one, in case an IFrame was being used.
```

As some modern browsers may block the alert() JavaScript function in specific locations, it may be handy to know a few other basic XSS payloads to verify the existence of XSS. One such XSS payload is <plaintext>, which will stop rendering the HTML code that comes after it and display it as plaintext. Another easy-to-spot payload is <script>print()</script> that will pop up the browser print dialog, which is unlikely to be blocked by any browsers. Try using these payloads to see how each works. You may use the reset button to remove any current payloads.
