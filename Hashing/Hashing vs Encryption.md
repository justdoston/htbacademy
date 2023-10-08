# Hashing

As hashing is a one-way process, the only way to attack it is to use a list containing possible passwords.
Each password from this list is hashed and compared to the original hash.
## SHA_512
SHA-512 converts a long string of characters into a hash value.
It is fast and efficient, but there are many rainbow table attacks where an attacker uses
a pre-computed table to reconstruct the original passwords.
## Blowfish
Conversely, Blowfish is a symmetric block cipher algorithm that encrypts a password with a key. It is more secure than SHA-512 but also a lot slower. 
BCrypt uses a slow hash function to make it harder for potential attackers to guess passwords or perform rainbow table attacks.
## Argon2
Argon2, on the other hand, is a modern and secure algorithm explicitly designed for password hashing systems. 
It uses multiple rounds of hash functions and a large amount of memory to make it harder for attackers to guess passwords.
This is considered one of the most secure algorithms because it has a high time and resource requirement.

**Example**
Example of md5 hashing
```bash
┌──(hunter㉿kali)-[~]
└─$echo -n "p@ssw0rd" | md5sum

0f359740bd1cda994f8b55330c86d845
```

# Encryption
Encryption is the process of converting data into a format in which the original content is not accessible. Unlike hashing, encryption is reversible,
i.e., it's possible to decrypt the ciphertext (encrypted data) and obtain the original content. 
Some classic examples of encryption ciphers are the Caesar cipher, Bacon's cipher and Substitution cipher. 
Encryption algorithms are of two types: Symmetric and Asymmetric.

Here is example of xor encryption with "academy" key:
```bash
┌──(hunter㉿kali)-[~]
└─$ python3
Python 3.11.5 (main, Aug 29 2023, 15:31:31) [GCC 13.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from pwn import xor
>>> xor("opens3same", "academy")
/home/hunter/.local/lib/python3.11/site-packages/pwnlib/util/fiddling.py:327: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  strs = [packing.flat(s, word_size = 8, sign = False, endianness = 'little') for s in args]
b'\x0e\x13\x04\n\x16^\n\x00\x0e\x04'
```
Decryption:
```bash
┌──(hunter㉿kali)-[~]
└─$ python3
Python 3.11.5 (main, Aug 29 2023, 15:31:31) [GCC 13.2.0] on linux
Type "help", "copyright", "credits" or "license" for more information.
>>> from pwn import xor
>>> xor('\x0e\x13\x04\n\x16^\n\x00\x0e\x04', "academy")
/home/hunter/.local/lib/python3.11/site-packages/pwnlib/util/fiddling.py:327: BytesWarning: Text is not bytes; assuming ASCII, no guarantees. See https://docs.pwntools.com/#bytes
  strs = [packing.flat(s, word_size = 8, sign = False, endianness = 'little') for s in args]
b'opens3same'
>>> 
```

