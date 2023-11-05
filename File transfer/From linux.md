# Base64

**Sender:** `cat file | base64 -w 0;echo` <br>
**Reciever** `echo -n base64payload | base64 -d > filename`   Confirm md5 hash match in linux: `md5sum file`

# Netcat
**Sender:** `nc 10.10.10.10 4444 < file`<br>
**Reciever:** `nc -lvp 4444 > file`


