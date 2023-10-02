# Vulnerability Assessment 

Vulnerability assessments involve running an automated scan of an environment to enumerate vulnerabilities. 
These can be authenticated or unauthenticated. No exploitation is attempted, but we will often look to validate scanner 
results so our report may show a client which scanner results are actual issues and which are false positives. 
Validation may consist of performing an additional check to confirm a vulnerable 
version is in use or a setting/misconfiguration is in place, but the goal is not to gain a foothold and move laterally/vertically. 
Some customers will even ask for scan results with no validation.

# Internal vs External

An external scan is performed from the perspective of an anonymous user on the internet targeting the organization's public systems. An internal scan is conducted from the perspective of a scanner on the internal network and investigates hosts from behind the firewall. This can be done from the perspective of an anonymous user on the corporate user network, emulating a compromised server, or any number of different scenarios. A customer may even ask for an internal scan to be conducted with credentials, which can lead to considerably more scanner findings to sift through but will also produce more accurate and less generic results.

# Penetration Testing

Penetration testing goes beyond automated scans and can leverage vulnerability scan data to help guide exploitation. Like vulnerability scans, these can be performed from an internal or external perspective. Depending on the type of penetration test (i.e., an evasive test), we may not perform any kind of vulnerability scanning at all.

A penetration test may be performed from various perspectives, such as "black box," where we have no more information than the name of the company during an external or a network connection for an internal, "grey box" where we are given just in-scope IP addresses/CIDR network ranges, or "white box" where we may be given credentials, source code, configurations, and more.

# Evasive Testing

Finally, we may be asked to perform evasive testing throughout the assessment. In this type of assessment, we will try to remain undetected for as long as possible and see what kind of access, if any, we can obtain while working stealthily. This can help to simulate a more advanced attacker. However, this type of assessment is often limited by time constraints that are not in place for a real-world attacker. A client may also opt for a longer-term adversary simulation that may occur over multiple months, with few company staff aware of the assessment and few or no client staff knowing the exact start day/time of the assessment. This 
assessment type is well-suited for more security mature organizations and requires a bit of a different skill set than a traditional network/application penetration tester.


# Answer of Questions
**What component of a report should be written in a simple to understand and non-technical manner?**

Answer: `executive summary`

**It is a good practice to name and recommend specific vendors in the component of the report mentioned in the last question. True or False?** 

Answer: `False`
