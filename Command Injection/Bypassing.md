# Using $IFS
Using the `($IFS)` Linux Environment Variable may also work since its default value is a space and a tab, which would work between command arguments. So, if we use `${IFS}` where the spaces should be, the variable should be automatically replaced with a space, and our command should work.
<br>
Let us use `${IFS}` and see if it works (127.0.0.1%0a${IFS}):

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/db622f74-4781-4f5c-818c-f4f628f9288c)
We see that our request was not denied this time, and we bypassed the space filter again.

## Using Brace Expansion
There are many other methods we can utilize to bypass space filters. For example, we can use the Bash Brace Expansion feature, which automatically adds spaces between arguments wrapped between braces, as follows:
```
dostonbek@htb[/htb]$ {ls,-la}

total 0
drwxr-xr-x 1 21y4d 21y4d   0 Jul 13 07:37 .
drwxr-xr-x 1 21y4d 21y4d   0 Jul 13 13:01 ..
```
## Advanced tech

For example, if we look at the $PATH environment variable in Linux, it may look something like the following:

```
dostonbek@htb[/htb]$ echo ${PATH}

/usr/local/bin:/usr/bin:/bin:/usr/games
```
So, if we start at the 0 character, and only take a string of length 1, we will end up with only the / character, which we can use in our payload:
```
dostonbek@htb[/htb]$ echo ${PATH:0:1}

/
```




