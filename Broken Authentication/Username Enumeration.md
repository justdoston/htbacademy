Popular web framework `WordPress` suffer from username enumeration. The development team chose to have a smoother UX by lowering the framework’s security level a bit.

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/bbb27e13-5310-4d95-bafa-05d437bcf519)

## User unknown attack

In wordpress or other web application we can easily enumerate username with response:
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/8ef3fe1a-1e3c-49d1-9c31-72260741f1d3)

We can carry out the brute force attack using wfuzz and a reverse string match against the response text 
( --hs "Unknown username," where "hs" should be a mnemonic used for string hiding), 
using a short wordlist from SecLists. Since we are not trying to find a valid password, we do not care about the Password field, so we will use a dummy one.

## Timing attack
There might be situation when application cheking username takes longer time than usual, because of code of backend.

Download the script timing.py to witness these types of timing differences and run it against an example web application (timing.php) that uses bcrypt. 
https://academy.hackthebox.com/storage/modules/80/scripts/timing_py.txt

```bash
┌──(hunter㉿kali)-[~]
└─$ python3 timing.py /usr/share/wordlists/seclists/Usernames/top-usernames-shortlist.txt
[-] Checking account root foobar
[+] user root            took 0.282388
[-] Checking account admin foobar
[+] user admin           took 0.310175
[-] Checking account test foobar
[+] user test            took 0.300373
[-] Checking account guest foobar
[+] user guest           took 0.283238
[-] Checking account info foobar
[+] user info            took 0.281789
[-] Checking account adm foobar
[+] user adm             took 0.317386
[-] Checking account mysql foobar
[+] user mysql           took 0.301636
[-] Checking account user foobar
[+] user user            took 0.28492
[-] Checking account administrator foobar
[+] user administrator   took 0.317271
[-] Checking account oracle foobar
[+] user oracle          took 0.300086
[-] Checking account ftp foobar
[+] user ftp             took 0.287675
[-] Checking account pi foobar
[+] user pi              took 0.31426
[-] Checking account puppet foobar
[+] user puppet          took 0.322768
[-] Checking account ansible foobar
[+] user ansible         took 0.283845
[-] Checking account ec2-user foobar
[+] user ec2-user        took 0.295656
[-] Checking account vagrant foobar
[+] user vagrant         took 0.49406
[-] Checking account azureuser foobar
[+] user azureuser       took 0.273907
```
as we can see user `vagrant` is valid, because it took too long.

## Enumerate usernames through Password Reset
Reset forms are often less well protected than login ones. Therefore, they very often leak information about a valid or invalid username. 
Like we have already discussed, an application that replies with a "You should receive a message shortly" when a valid username has been found and "Username unknown,
check your data" for an invalid entry leaks the presence of registered users.

## Registratin vulnerability
Sometime web applications registration page leads to username enumeration, because we can't register 2 user into 1 username
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/108a5dde-d155-4dcd-8578-74080cfa1a41)

This is how I enumerate username...

