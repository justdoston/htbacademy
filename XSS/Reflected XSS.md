# Reflected XSS
There are two types of Non-Persistent XSS vulnerabilities: Reflected XSS, which gets processed by the back-end server, and DOM-based XSS, which is completely processed on the client-side and never reaches the back-end server. Unlike Persistent XSS, Non-Persistent XSS vulnerabilities are temporary and are not persistent through page refreshes. Hence, our attacks only affect the targeted user and will not affect other users who visit the page.

If we visit the Reflected page again, the error message no longer appears, and our XSS payload is not executed, which means that this XSS vulnerability is indeed Non-Persistent.

But if the XSS vulnerability is Non-Persistent, how would we target victims with it?

This depends on which HTTP request is used to send our input to the server. We can check this through the Firefox Developer Tools by clicking [CTRL+I] and selecting the Network tab. Then, we can put our test payload again and click Add to send it:
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/88bdf3a2-629b-43b9-86fe-7614f2cc6334)

As we can see, the first row shows that our request was a GET request. GET request sends their parameters and data as part of the URL. So, to target a user, we can send them a URL containing our payload. To get the URL, we can copy the URL from the URL bar in Firefox after sending our XSS payload, or we can right-click on the GET request in the Network tab and select Copy>Copy URL. Once the victim visits this URL, the XSS payload would execute:

