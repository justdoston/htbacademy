# Weak NFS Privileges
Network File System (NFS) allows users to access shared files or directories over the network hosted on Unix/Linux systems. NFS uses TCP/UDP port 2049. Any accessible mounts can be listed remotely by issuing the command `showmount -e`, which lists the NFS server's export list (or the access control list for filesystems) that NFS clients.
```
dostonbek@htb[/htb]$ showmount -e 10.129.2.12

Export list for 10.129.2.12:
/tmp             *
/var/nfs/general *
```
**NFS Option**
## root_squash
If the root user is used to access NFS shares, it will be changed to the nfsnobody user, which is an unprivileged account. Any files created and uploaded by the root user will be owned by the nfsnobody user, which prevents an attacker from uploading binaries with the SUID bit set.
