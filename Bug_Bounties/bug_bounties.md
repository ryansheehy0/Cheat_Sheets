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
	- [3 Golden Rules](#3-golden-rules)
	- [Bug Bounty Platforms](#bug-bounty-platforms)
	- [What to look out for](#what-to-look-out-for)
	- [Good attack targets](#good-attack-targets)
	- [Tools](#tools)
		- [Programs](#programs)
		- [Tool websites](#tool-websites)
		- [Browser extentions](#browser-extentions)
		- [Need to research](#need-to-research)
	- [Important terms](#important-terms)

<!-- /TOC -->

## [3 Golden Rules](#table-of-contents)
1. Testing for vulnerabilities should not degrade, damage, or destroy the application for other users.
1. Report vulnerabilities without any conditions attached.
1. Do not share any vulnerabilities to 3rd parties.

- Make sure to read all of the requirements before beginning bug bountying.

## [Bug Bounty Platforms](#table-of-contents)
- https://www.hackerone.com/
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

## [What to look out for](#table-of-contents)
- [Recon](./recon.md)
- Look through source code
	- Comments with sensitive info
	- Check for max length of form inputs
- Parameters to files
	- [Path traversal](./path_traversal.md)
- User input that would use the db
	- [SQL injection](./sql_injection.md)
	- NoSQL injection
- User ids
	- [IDORs](./insecure_direct_object_references.md)
- URL parameters that output to the DOM or User inputs that are saved to the db and can be seen by other users.
	- [XSS](./cross_site_scripting.md)
- Unaccessible pages and URL/URL paths as arguments
	- [SSRF](./server_side_request_forgery.md)
- Login pages
	- Brute force attack with common usernames and passwords
- Malicious action, cookie based session handling, and predictable arguments.
	- [CSRF](./cross_site_request_forgery.md)
- Client sends XML to server
	- [XXE](./xml_external_entities.md)

- GraphQL attacks
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

You often need 2 accounts in order to perform certain attacks. An attacking account and a victim account.
- Stored XSS
- IDORs

## [Good attack targets](#table-of-contents)
- Not up to date webpages
- Powered by a 3rd party company
	- Wordpress, GoDaddy, Wix
- Foreign languages. Less people search for bugs there.

## [Tools](#table-of-contents)

### [Programs](#table-of-contents)
Tools:
1. Burp suit: Intercepts requests made from the client to the server.
- [Burp-UserAgent](https://github.com/codewatchorg/Burp-UserAgent). Certain bug bounties may required info be appended to user agents.
- Settings -> Tasks -> New resource pool -> Set maximum concurrent requests
1. Shodan: A database of all open IP addresses.
1. Wayback machine: A database of snapshots of different URLS from different points in time.
1. amass: Find subdomains and ip addresses used by domain

### [Tool websites](#table-of-contents)
- [URL Decoder/Encoder](https://meyerweb.com/eric/tools/dencoder/)
- [JavaScript Deobfuscator](https://deobfuscate.io/)
- [ASCII table](https://www.asciitable.com/)
- [CSRF HTML generator](https://tools.nakanosec.com/csrf/)
- [get your user agent](https://www.whatsmyua.info/)

### [Browser extentions](#table-of-contents)
- Wappalyzer
	- Technologies used to create the website
- IP Address and Domain Information
- Multiple Url Opener

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

## [Important terms](#table-of-contents)

| Term       | Definition                                                                 |
|------------|----------------------------------------------------------------------------|
| User Agent | Information about the user. Such as their OS, browser, and their versions. |