We can detect SSTI vulnerabilities by injecting different tags in the inputs we control to see if they are evaluated in the response. 
We don't necessarily need to see the injected data reflected in the response we receive. Sometimes it is just evaluated on different pages (blind).

Easiest way injecting these to input:
```bash
{7*7}
${7*7}
#{7*7}
%{7*7}
{{7*7}}
...
```
We will look for "49" in the response when injecting these payloads to identify that server-side evaluation occurred.

The diagram below from PortsSwigger can help us identify if we are dealing with an SSTI vulnerability and also identify the underlying template engine.

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/b7492858-5fdf-4b83-97b2-94addd4f3640)


In addition to the above diagram, we can try the following approaches to recognize the technology we are dealing with:

    Check verbose errors for technology names. Sometimes just copying the error in Google search can provide us with a straight answer regarding the underlying technology used
    Check for extensions. For example, .jsp extensions are associated with Java. When dealing with Java, we may be facing an expression language/OGNL injection vulnerability instead of traditional SSTI
    Send expressions with unclosed curly brackets to see if verbose errors are generated. Do not try this approach on production systems, as you may crash the webserver.
