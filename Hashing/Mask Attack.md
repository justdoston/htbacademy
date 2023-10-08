# Mask Attack
Mask attacks are used to generate words matching a specific pattern. 
This type of attack is particularly useful when the password length or format is known. 
A mask can be created using static characters, ranges of characters (e.g. [a-z] or [A-Z0-9]), or placeholders.

```bash
Placeholder 	         Meaning
?l 	          lower-case ASCII letters (a-z)
?u 	          upper-case ASCII letters (A-Z)
?d 	          digits (0-9)
?h 	          0123456789abcdef
?H 	          0123456789ABCDEF
?s 	          special characters («space»!"#$%&'()*+,-./:;<=>?@[]^_`{
?a 	          ?l?u?d?s
?b 	          0x00 - 0xff
```
The above placeholders can be combined with options "-1" to "-4" which can be used for custom placeholders. 
See the Custom charsets section here for a detailed breakdown of each of these four command-line parameters that can be used to configure four custom charsets.

For example: password is -> ILFREIGHTabcxy2015

Mask attack:
```bash
hashcat -a 3 -m 0 md5_mask_example_hash -1 01 'ILFREIGHT?l?l?l?l?l20?1?d'
```
The `-1` option was used to specify a placeholder with just 0 and 1. Hashcat could crack the hash in 43 seconds on CPU power. 
The `--increment` flag can be used to increment the mask length automatically 
with a length limit that can be supplied using the `--increment-max` flag.

## Task
Crack the following MD5 hash using a mask attack: 50a742905949102c961929823a2e8ca0. 
Use the following mask: -1 02 'HASHCAT?l?l?l?l?l20?1?d'
## Solve
```bash
hashcat -a 3 -m 0 50a742905949102c961929823a2e8ca0 -1 02 'HASHCAT?l?l?l?l?l20?1?d'
```
**Response**
```bash
50a742905949102c961929823a2e8ca0:HASHCATqrstu2020         
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 0 (MD5)
Hash.Target......: 50a742905949102c961929823a2e8ca0
Time.Started.....: Sun Oct  8 20:16:36 2023 (19 secs)
Time.Estimated...: Sun Oct  8 20:16:55 2023 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Mask.......: HASHCAT?l?l?l?l?l20?1?d [16]
Guess.Charset....: -1 02, -2 Undefined, -3 Undefined, -4 Undefined 
Guess.Queue......: 1/1 (100.00%)
Speed.#1.........:  2287.5 kH/s (0.68ms) @ Accel:1024 Loops:1 Thr:1 Vec:16
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 40222720/237627520 (16.93%)
Rejected.........: 0/40222720 (0.00%)
Restore.Point....: 40218624/237627520 (16.93%)
Restore.Sub.#1...: Salt:0 Amplifier:0-1 Iteration:0-1
Candidate.Engine.: Device Generator
Candidates.#1....: HASHCATinnac2020 -> HASHCATmepem2020
Hardware.Mon.#1..: Temp: 50c Util: 56%

Started: Sun Oct  8 20:15:58 2023
Stopped: Sun Oct  8 20:16:56 2023
```

