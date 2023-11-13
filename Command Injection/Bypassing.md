# Using $IFS
Using the `($IFS)` Linux Environment Variable may also work since its default value is a space and a tab, which would work between command arguments. So, if we use `${IFS}` where the spaces should be, the variable should be automatically replaced with a space, and our command should work.
<br>
Let us use `${IFS}` and see if it works (127.0.0.1%0a${IFS}):

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/db622f74-4781-4f5c-818c-f4f628f9288c)
We see that our request was not denied this time, and we bypassed the space filter again.
