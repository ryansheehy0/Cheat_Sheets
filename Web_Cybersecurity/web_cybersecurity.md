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

# Web Cybersecurity

These notes help to solve the problem of a lack of comprehensive organization for web cybersecurity.

## Table of Contents

<!-- TOC -->

- [Web Cybersecurity](#web-cybersecurity)
	- [Table of Contents](#table-of-contents)
	- [Need to study resources](#need-to-study-resources)
	- [Bug Bounty Platforms](#bug-bounty-platforms)
	- [Attacks](#attacks)
	- [Tools](#tools)
		- [Need to research](#need-to-research)
		- [Websites](#websites)
		- [Browser extensions](#browser-extensions)
	- [Important terms](#important-terms)

<!-- /TOC -->

## [Need to study resources](#table-of-contents)
- Labs:
	- https://app.hackinghub.io/hubs
	- https://portswigger.net/web-security/dashboard
	- https://tryhackme.com/
	- https://www.hackthebox.com/
	- https://capturetheflag.withgoogle.com/
- Prevent XSS: https://www.geeksforgeeks.org/cross-site-scripting-xss-prevention-techniques/
- OWASP(Open Web Application Security Project) cheat sheet: https://cheatsheetseries.owasp.org/
- Reddit XSS: https://www.reddit.com/r/xss/
- Rs0n:
	- Website: https://ars0nsecurity.com/
	- Github notes: https://github.com/R-s0n
- Github seclist: https://github.com/danielmiessler/SecLists
- Javascript for hackers book: https://www.realmit.eu/storage/bookdumpo/Gareth_Heyes_-_JavaScript_for_hackers_Learn_to_think_like_a_hacker_2022_Lean_Publishing.pdf
- Get around firebase: https://github.com/0xbigshaq/firepwn-tool
- Pico CTFs: https://www.picoctf.org/
- XSS Validator: https://github.com/PortSwigger/xss-validator

## [Bug Bounty Platforms](#table-of-contents)
- https://hackerone.com/opportunities/all

- https://www.intigriti.com/
- Bugbounter
- https://www.bugcrowd.com/
- NordicDefender Bug Bounty
- SafeHats
- HackenProof
- Synack
- SecureBug
- Open Bug Bounty
- YesWeHack
- Topcoder, a Wipro company
- Cobalt
- BountyFactory
- Zerocopter

## [Attacks](#table-of-contents)
- Look through source code
	- Comments with sensitive info
	- Check for max length on form inputs
- URL parameters to files
	- [Path traversal](./path_traversal.md)
- URL parameters that output to the DOM or User inputs that are saved to the db and can be seen by other users.
	- [XSS](./cross_site_scripting.md)
- User input that would use the db
	- [SQL injection](./sql_injection.md)
	- NoSQL injection
- User ids
	- [IDORs](./insecure_direct_object_references.md)
- URL/URL paths as arguments or parameters to files
	- Unaccessible pages
		- [SSRF](./server_side_request_forgery.md)
- Login pages
	- Brute force attack with common usernames and passwords
- Malicious action, cookie based session handling, and predictable arguments.
	- [CSRF](./cross_site_request_forgery.md)
- Client sends XML to server, XML processed on the server, or accepts XML like files(SVG, DOCX, etc)
	- [XXE](./xml_external_entities.md)

- GraphQL attacks
- Improper access control
- Authoritative Zone Transfer(AXFR) on port 53
- Default credentials and Insecure server configurations
	- s3 bucket
- Business logic errors(BLEs)
- File upload vulnerabilities
- CNAME takeover
	- If there is a CNAME that isn't being used, you can get that url and create your own phishing website.
	- How do you discover all the CNAMEs someone has for the domain name?
- JWT attacks
- Broken objects level authorization(BOLA)
- Broken access control
- 403 bypass
- API Enumeration
- LFI and RFI
- Wordpress and CMS
- How to hack APIs
- LDAP injection
- Email which opened gets ip address/location
- CDN(Content delivery networks) vulnerabilities?

You often need 2 accounts in order to perform certain attacks. An attacking account and a victim account.
- Stored XSS
- IDORs

## [Tools](#table-of-contents)

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
- wfuzz
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
- Shodan
	- Database of all open IP addresses
- Wayback machine
	- Database of snapshots of deferent URLs from different points in time
- amass
	- Finds subdomains and ip addresses used by domain

### [Websites](#table-of-contents)
- [URL Decoder/Encoder](https://meyerweb.com/eric/tools/dencoder/)
- [JavaScript Deobfuscator](https://deobfuscate.io/)
- [HTML character code table](https://www.rapidtables.com/web/html/html-codes.html)
- [CSRF HTML generator](https://tools.nakanosec.com/csrf/)
- [Get your user agent](https://www.whatsmyua.info/)
- [JSFuck](https://jsfuck.com/)

### [Browser extensions](#table-of-contents)
- Google translate
- Quick source viewer
- React Developer Tools
- Wappalizer

- IP Address and Domain Information
- Multiple Url Opener

## [Important terms](#table-of-contents)

| Term       | Definition                                                                 |
|------------|----------------------------------------------------------------------------|
| User Agent | Information about the user. Such as their OS, browser, and their versions. |