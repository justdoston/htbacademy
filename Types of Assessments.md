# Vulnerability Assessment 

Vulnerability assessments involve running an automated scan of an environment to enumerate vulnerabilities. 
These can be authenticated or unauthenticated. No exploitation is attempted, but we will often look to validate scanner 
results so our report may show a client which scanner results are actual issues and which are false positives. 
Validation may consist of performing an additional check to confirm a vulnerable 
version is in use or a setting/misconfiguration is in place, but the goal is not to gain a foothold and move laterally/vertically. 
Some customers will even ask for scan results with no validation.
