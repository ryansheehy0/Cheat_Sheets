[Home](../README.md)

# Javascript Bug Bounties

## Table of Contents

<!-- TOC -->

- [Javascript Bug Bounties](#javascript-bug-bounties)
	- [Table of Contents](#table-of-contents)
	- [Rules](#rules)
	- [Links](#links)
	- [Places to look](#places-to-look)
	- [How to find the source code?](#how-to-find-the-source-code)
	- [Static Analysis Security TestingSAST tools](#static-analysis-security-testingsast-tools)
	- [Useful Terms](#useful-terms)
	- [SQL Injection](#sql-injection)
	- [Cross site scriptingXSS](#cross-site-scriptingxss)
	- [Authentication and Authorizations attacks](#authentication-and-authorizations-attacks)
	- [File upload vulnerabilities](#file-upload-vulnerabilities)
	- [Server side request forgeriesSSRF](#server-side-request-forgeriesssrf)
	- [Cross-Site Request ForgeryCSRF](#cross-site-request-forgerycsrf)
	- [Insecure Deserialization](#insecure-deserialization)
	- [Insecure Direct Object ReferencesIDOR](#insecure-direct-object-referencesidor)
	- [Leaked Credentials](#leaked-credentials)
	- [Steps](#steps)

<!-- /TOC -->

## [Rules](#table-of-contents)
- Testing for vulnerabilities should not degrade, damage, or destroy(No DDOS)
- Report vulnerabilities without any conditions attached
- Do not share any vulnerabilities to 3rd parties

- Production servers are off-limits.

- Certain links are out of scope
- System downtime is not permitted under any circumstances.
  - Any form of DDoS or DoS is prohibited.
  - Use of any harmful malware is prohibited; this includes ransomware and other variations
- Exfiltration of Personal Identifiable Information(PII) is prohibited.


## [Links](#table-of-contents)
- https://www.hackerone.com/
- https://www.bugcrowd.com/
- https://www.intigriti.com/

## [Places to look](#table-of-contents)
- Sub domains
- Google DOB


- Lack of input validation
- Lack of output encoding
- Midding access control
- Weak regex checks
- Server side request forgeries
- Open redirects


## [How to find the source code?](#table-of-contents)
  - Look at the client side code
  - Reverse engineer the source code
  - Github, pastebin, wayback machine

## [Static Analysis Security Testing(SAST) tools](#table-of-contents)
  - Can have false positives or false negatives.
    - Need to always manually check

## [Useful Terms](#table-of-contents)

| Term                       | Description |
|----------------------------|-------------|
| Privilege escalation       |             |
| Remote Code Execution(RCE) |             |
| I/O doors                  |             |
| Missing access controls    |             |

**0 day exploit** is an exploit that the target has had zero days of knowing about that vulnerability.

## [SQL Injection](#table-of-contents)
## [Cross site scripting(XSS)](#table-of-contents)
  - Used to run unwanted javascript on the server itself. This is useful because it allows you to bypass permissions because the javascript is running on the server itself.
## [Authentication and Authorizations attacks](#table-of-contents)
- User permissions in applications
## [File upload vulnerabilities](#table-of-contents)
## [Server side request forgeries(SSRF)](#table-of-contents)
## [Cross-Site Request Forgery(CSRF)](#table-of-contents)
## [Insecure Deserialization](#table-of-contents)
## [Insecure Direct Object References(IDOR)](#table-of-contents)
## [Leaked Credentials](#table-of-contents)

JWT attacks
BOLA broken objects level authorization

## [Steps](#table-of-contents)
- Recon: gain info
- Weaponization: Combine the objective with an exploit. 
- Delivery: How will the weaponized function be delivered to the target	
- Exploitation: Exploit the target's system to execute code
- Installation: Install malware or other tooling
- Command & Control: Control the compromised asset from a remote central controller
- Actions on Objectives: Any end objectives: ransomware, data exfiltration, etc.