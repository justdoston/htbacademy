Sometimes, hashes are stored in certain formats. For example, hash:salt or $id$salt$hash.

The hash `2fc5a684737ce1bf7b3b239df432416e0dd07357:2014` is a SHA1 hash with the salt of 2014.

The hash `$6$vb1tLY1qiY$M.1ZCqKtJBxBtZm1gRi8Bbkn39KU0YJW1cuMFzTRANcNKFKR4RmAQVk4rqQQCkaJT6wXqjUkFcA/qNxLyqW.U/` 
contains three fields delimited by `$`, where the first field is the id, i.e., 6. 
This is used to identify the type of algorithm used for hashing. The following list contains some ids and their corresponding algorithms.
```bash
$1$  : MD5
$2a$ : Blowfish
$2y$ : Blowfish, with correct handling of 8 bit characters
$5$  : SHA256
$6$  : SHA512
```
# Hashid
Hashid is a Python tool, which can be used to detect various kinds of hashes. 
At the time of writing, hashid can be used to identify over 200 unique hash types, and for others, it will make a best-effort guess, 
which will still require some additional work to narrow it down. The full list of supported hashes can be found here. It can be installed using pip.

##Installing
`pip3 install hashid`

**Basic** running:
```bash
┌──(hunter㉿kali)-[~]
└─$ hashid '$apr1$71850310$gh9m4xcAn3MGxogwX/ztb.'
Analyzing '$apr1$71850310$gh9m4xcAn3MGxogwX/ztb.'
[+] MD5(APR) 
[+] Apache MD5
```
Using hashid for **list** of hashes:
```bash
dostonbek@htb[/htb]$ hashid hashes.txt 

--File 'hashes.txt'--
Analyzing '2fc5a684737ce1bf7b3b239df432416e0dd07357:2014'
[+] SHA-1 
[+] Double SHA-1 
[+] RIPEMD-160 
[+] Haval-160 
[+] Tiger-160 
[+] HAS-160 
[+] LinkedIn 
[+] Skein-256(160) 
[+] Skein-512(160) 
[+] Redmine Project Management Web App 
[+] SMF ≥ v1.1 
Analyzing '$P$984478476IagS59wHZvyQMArzfx58u.'
[+] Wordpress ≥ v2.6.2 
[+] Joomla ≥ v2.5.18 
[+] PHPass' Portable Hash 
--End of file 'hashes.txt'--
```
If known, **hashid** can also provide the corresponding Hashcat hash mode with the `-m` flag if it is able to determine the hash type.
```bash
┌──(hunter㉿kali)-[~]
└─$ hashid '$DCC2$10240#tom#e4e938d12fe5974dc42a90120bd9c90f' -m
Analyzing '$DCC2$10240#tom#e4e938d12fe5974dc42a90120bd9c90f'
[+] Domain Cached Credentials 2 [Hashcat Mode: 2100]
```
Context is also important with source...
