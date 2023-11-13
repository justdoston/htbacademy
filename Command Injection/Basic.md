# Command Injection Methods

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/ccfe7d9d-e002-40d8-a1d4-885f8acf609b)

We can use any of these operators to inject another command so **both** or **either** of the commands get executed. **We would write our expected input (e.g., an IP), then use any of the above operators, and then write our new command.**

`
Tip: In addition to the above, there are a few unix-only operators, that would work on Linux and macOS, but would not work on Windows, such as wrapping our injected command with double backticks (``) or with a sub-shell operator ($()).
`<br><br>
In general, for basic command injection, all of these operators can be used for command injections **regardless of the web application language, framework, or back-end server**. So, if we are injecting in a **PHP** web application running on a **Linux** server, or a **.Net** web application running on a **Windows** back-end server, or a **NodeJS** web application running on a **macOS** back-end server, our injections should work **regardless**.

`Note: The only exception may be the semi-colon ;, which will not work if the command was being executed with Windows Command Line (CMD), but would still work if it was being executed with Windows PowerShell.`

