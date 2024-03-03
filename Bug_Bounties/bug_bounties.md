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
	- [Check list](#check-list)
	- [Good attack targets](#good-attack-targets)
	- [Tools](#tools)
		- [Need to research](#need-to-research)

<!-- /TOC -->

## [Rules](#table-of-contents)
1. Testing for vulnerabilities should not degrade, damage, or destroy the application for other users.
1. Report vulnerabilities without any conditions attached.
1. Do not share any vulnerabilities to 3rd parties.

## [Links](#table-of-contents)
- https://www.hackerone.com/
- https://www.bugcrowd.com/
- https://www.intigriti.com/

## [Check list](#table-of-contents)
1. [Recon](./recon.md)
1. Look through source code
1. [Path traversal](./path_traversal.md)
1. [SQL injection](./sql_injection.md)
1. [IDORs](./idor.md)
1. [XSS](./cross_site_scripting.md)

- Cross-site scripting(XSS)
	- Used to run unwanted javascript on the server itself. This is useful because it allows you to bypass permissions because the javascript is running on the server itself.
- Cross site request forgery(CSRF)
- Server side request forgery(SSRF)
- XML External Entity (XXE)
- Default credentials and Insecure server configurations
- Authoritative Zone Transfer(AXFR) on port 53
- Business logic errors(BLEs)
- File upload vulnerabilities
- CNAME takeover
	- If there is a CNAME that isn't being used, you can get that url and create your own phishing website.
	- How do you discover all the CNAMEs someone has for the domain name?
- JWT attacks
- Broken objects level authorization(BOLA)
- Brute force attacks on admin accounts with common passwords
- Broken access control
- Check for max length of form inputs

You often need 2 different accounts:
- Attacker and victim account
	- Used to test Stored XSS attacks
	- IDOR vulnerabilities

## [Good attack targets](#table-of-contents)
- Not up to date dates
- Powered by a 3rd party company
	- Wordpress, GoDaddy, Wix

## [Tools](#table-of-contents)
Tools:
1. Burp suit: Intercepts requests made from the client to the server.
1. Shodan: A database of all open IP addresses.
1. Wayback machine: A database of snapshots of different URLS from different points in time.

### [Need to research](#table-of-contents)
- Wireshark
- John the ripper(Brute force attacker)
- sqlmap
- Aircrack ng
- net cat
- nmap
	- Search which ports are open for an IP Address
- nikto
- metasploit
- Hashcat
- Hydra
	- Automated brute force attacker
- Maltego
- OWASP ZAP
- wfuz
	- Sub domain fuzzing
- dig
	- Used for finding AXFRs
- nslookup
- whois
- theHarvester
- crt.sh
- httprobe
	- Valid urls
- Hakrawler
	- Actively searches for paths and subdomains
		- Checks wayback machine, spiders application, parses robots.txt and sitemap.xml
		- Spider is crawling through a website and seeing any domains linked to it
- gau
	- get all urls. Uses AlienVault's Open Threat Exchange, wayback machine, common crawl and URLScan
	- Just accesses database and doesn't crawl(like a spider)
