<!--
 * This file is part of RS Cheat Sheets.
 *
 * RS Cheat Sheets is free software: you can redistribute it and/or modify
 * it under the terms of the GNU General Public License as published by
 * the Free Software Foundation, either version 3 of the License, or
 * (at your option) any later version.
 *
 * RS Cheat Sheets is distributed in the hope that it will be useful,
 * but WITHOUT ANY WARRANTY; without even the implied warranty of
 * MERCHANTABILITY or FITNESS FOR A PARTICULAR PURPOSE.  See the
 * GNU General Public License for more details.
 *
 * You should have received a copy of the GNU General Public License
 * along with RS Cheat Sheets. If not, see <https://www.gnu.org/licenses/>.
 */
-->

[Home](../README.md)

# Bug Bounties

## Table of Contents

<!-- TOC -->

- [Bug Bounties](#bug-bounties)
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
	- No DDOS, messing with other user's accounts, or no harmful malware.
- Report vulnerabilities without any conditions attached
- Do not share any vulnerabilities to 3rd parties

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