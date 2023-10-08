# Hybrid Mode
Hybrid mode is a variation of the combinator attack, wherein multiple modes can be used together for a fine-tuned wordlist creation.
This mode can be used to perform very targeted attacks by creating very customized wordlists. 
It is particularly useful when you know or have a general idea of the organization's password policy or common password syntax. 
The attack mode for the hybrid attack is `6`.

Let's consider a password such as `football1$`. The example below shows how a wordlist can be used in combination with a mask.

Hashcat reads words from the wordlist and appends a unique string based on the mask supplied. In this case, the mask `?d?s` 
tells hashcat to append a digit and a special character at the end of each word in the rockyou.txt wordlist.

**Examples**
```bash
hashcat -a 6 -m 0 hash rockyou.txt '?d?s'
```
`?d` for numbers and `?s` special characters.
Attack mode `7` can be used to prepend characters to words using a given mask. 
The following example shows a mask using a custom character set to add a prefix to each word in the rockyou.txt wordlist. 
The custom character mask `20?1?d` with the custom character set
`-1 01` will prepend various years to each word in the wordlist (i.e., 2010, 2011, 2012..).

```bash
hashcat -a 7 -m 0 hash -1 01 '20?1?d'
```
## Task
Crack the following hash: `978078e7845f2fb2e20399d9e80475bc1c275e06` using the mask `?d?s`
**Solve**
```bash
hashcat -a 6 -m 100 978078e7845f2fb2e20399d9e80475bc1c275e06 /usr/share/wordlists/rockyou.txt -1 01 '?d?s'
```
Respone:
```bash
978078e7845f2fb2e20399d9e80475bc1c275e06:hybridmaster9$   
                                                          
Session..........: hashcat
Status...........: Cracked
Hash.Mode........: 100 (SHA1)
Hash.Target......: 978078e7845f2fb2e20399d9e80475bc1c275e06
Time.Started.....: Sun Oct  8 20:31:49 2023 (7 mins, 7 secs)
Time.Estimated...: Sun Oct  8 20:38:56 2023 (0 secs)
Kernel.Feature...: Pure Kernel
Guess.Base.......: File (/usr/share/wordlists/rockyou.txt), Left Side
Guess.Mod........: Mask (?d?s) [2], Right Side
Guess.Charset....: -1 01, -2 Undefined, -3 Undefined, -4 Undefined
Speed.#1.........:  5807.6 kH/s (7.01ms) @ Accel:32 Loops:330 Thr:1 Vec:16
Recovered........: 1/1 (100.00%) Digests (total), 1/1 (100.00%) Digests (new)
Progress.........: 2473489920/4733647050 (52.25%)
Rejected.........: 0/2473489920 (0.00%)
Restore.Point....: 7495296/14344385 (52.25%)
Restore.Sub.#1...: Salt:0 Amplifier:0-330 Iteration:0-330
Candidate.Engine.: Device Generator
Candidates.#1....: hybridtheory14471. -> hyathak6}
Hardware.Mon.#1..: Temp: 53c Util: 94%

Started: Sun Oct  8 20:31:16 2023
Stopped: Sun Oct  8 20:38:58 2023
```


