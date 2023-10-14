Even though CAPTCHA has been successfully bypassed in the past, it is still quite effective against automated attacks. 
An application should at least require a user to solve a CAPTCHA after a few failed attempts. 
Some developers often skip this protection altogether, and others prefer to present a CAPTCHA after some failed logins to retain a good user experience.

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/e3c62caf-585a-4b78-940b-8cbb07205094)


As an attacker, we can just read the page's source code to find the CAPTCHA code's value and bypass the protection. We should always read the source.

As developers, we should not develop our own CAPTCHA but rely on a well-tested one and require it after very few failed logins.

## Conclusion:
Second weak protection is blocking!

Sometime developers make incorrect desicion to block source IP, hacker can bypass it. For example following task not credentials IP more needed.

## Task
Work on webapp at URL /question2/ and try to bypass the login form using one of the method showed. What is the flag?

I tried to do a lot of thing, I copied request as curl, I tried to brute force with burp suite, hydra to find credentials, but failed, because it was rabbit hole. I tried to
understand task, Website doesn't accepting anything from outside, I mean website blocking public IP addresses. It just doesn't trust any IP from outside. 

So, as a hacker to bypass it we have to make request as if coming from inside (I mean private IP)
I tried to send curl and added extra header called `X-Forwarded-For: 127.0.0.1` after this header web application think request coming from 127.0.0.1 and allows us to bypass :)

```bash
curl -s -X POST http://94.237.62.174:52949/question2/ -H "X-Forwarded-For: 127.0.0.1"
```
