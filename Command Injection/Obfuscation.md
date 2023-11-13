# Linux & Windows
One very common and easy obfuscation technique is inserting certain characters within our command that are usually ignored by command shells like Bash or PowerShell and will execute the same command as if they were not there. Some of these characters are a single-quote `'` and a double-quote `"`, in addition to a few others.

**For example:**
```
┌──(hunter㉿kali)-[~]
└─$ w'h'oam'i'
hunter
```

```
┌──(hunter㉿kali)-[~]
└─$ w"h"oam"i"
hunter
```
The important things to remember are that `we cannot mix types of quotes and the number of quotes must be even`. We can try one of the above in our payload `(127.0.0.1%0aw'h'o'am'i)` and see if it works:

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/a317fa0d-8f3c-4c4d-bcba-aff63fa20538)
