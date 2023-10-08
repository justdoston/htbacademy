# Combination Attack
Combination attack for 2 word mixed passwords.
Like this:

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/e068b165-021e-4ac2-9c56-31470eaa34f3)

We can use `--stdout` flag from hashcat to mix wordlists:
```bash
hashcat -a 1 --stdout file1 file2
```
## Hashcat syntax
```bash
hashcat -a 1 -m <hash type> <hash file> <wordlist1> <wordlist2>
```

