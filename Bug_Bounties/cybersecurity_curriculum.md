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

- Tools
	- Wireshark
	- John the ripper(Brute force attacker)
	- sqlmap
	- Aircrack ng
	- burp suit
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
	- Shodan
		- Searches all ip addresses. Some data maybe outdated.
	- wfuz
		- Sub domain fuzzing
	- dig
		- Used for finding AXFRs
	- nslookup
	- whois
	- theHarvester
	- crt.sh
	- wayback machine
	- httprobe
		- Valid urls
	- Hakrawler
		- Actively searches for paths and subdomains
			- Checks wayback machine, spiders application, parses robots.txt and sitemap.xml
			- Spider is crawling through a website and seeing any domains linked to it
	- gau
		- get all urls. Uses AlienVault's Open Threat Exchange, wayback machine, common crawl and URLScan
		- Just accesses database and doesn't crawl(like a spider)
- Web security vulnerabilities
	- Insecure Direct Object References(IDOR)
	- SQL Injection(SQLI)
	- Cross-site scripting(XSS)
	- Cross site request forgery(CSRF)
	- Server side request forgery(SSRF)
	- XML External Entity (XXE)
	- Default credentials and Insecure server configurations
	- Authoritative Zone Transfer(AXFR) on port 53
	- Business logic errors(BLEs)
	- CNAME takeover
		- If there is a CNAME that isn't being used, you can get that url and create your own phishing website.
		- How do you discover all the CNAMEs someone has for the domain name?
- Recon
	- Find hidden URLs
- Browser tools

Bug bounty check list:
1. Find all open subdomains and paths that are in scope
	- example.com/robots.txt which tells crawls not to search in those paths
1. Inspect element and check for hidden HTML elements and comments with sensitive information
1. Check IDORs
	- Check HTML and CSS source code
		- Hidden HTML Elements
		- Comments with sensitive information
		- URLs in the CSS
	- Check if any urls have any parameters
	- Check if there is any information in the cookies
	- Check for any unused CNAMEs
1. Check SQL Injection on any inputs
1. Check any path traversals for any filename inputs.

Bug bounty check list:
1. Find open subdomains and paths that are in scope
1. Look through source code
1. Path traversal
1. SQL injection
1. IDORs