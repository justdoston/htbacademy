## Generating hash list using password list

```bash
for i in $(cat words); do echo -n $i | sha1sum | tr -d ' -';done
```

## Generating ntlm hash:

```bash
┌──(hunter㉿kali)-[~]
└─$ python3              
Python 3.11.5 (main, Aug 29 2023, 15:31:31) [GCC 13.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> import hashlib,binascii
>>> hash = hashlib.new('md4', "Password01".encode('utf-16le')).digest()
>>> print (binascii.hexlify(hash))
b'7100a909c7ff05b266af3c42ec058c33'
```
Ntlm hash of `Password01` is  `7100a909c7ff05b266af3c42ec058c33`
