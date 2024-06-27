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

Need to research:
- https://ivre.rocks/
- WHOIS info
- SSL/TLS certicate details
- Brute force
	- ShuffleDNS Standard
	- ShuffleDNS CeWL
- Link crawling
- param miner burp suit
- Burp suit -> target -> Site map
- ffuf
	- https://www.youtube.com/watch?v=0v1CTSyRpMU

# Recon
Finding all the open subdomains and paths that are in scope.

You can find the ip address of a domain with `host domain.com`

For some of these tools you need to kali repos in apt.
1. Create file in /etc/apt/sources.list.d called kali.list. `sudo touch /etc/apt/sources.list.d/kali.list`
1. Add `deb https://http.kali.org/kali kali-rolling main non-free contrib` to kali.list
1. Run `sudo apt update`. You should see a GPG error.
1. Download `https://archive.kali.org/archive-key.asc`
1. Move archive-key.asc to /etc/apt/trusted.gpg.d
1. Run `sudo apt update`

## Things to check
- domain.com/robots.txt
	- information on what web crawlers should exclude or include with their search
- domain.com/sitemap.xml
	- lists all the different paths for the website

## Finding subdomains
- `sublister -d domain.com`
- `amass enum -d domain.com`

Need to research
- `assetFinder`
-	`wayback machine`
- `Subfinder -d domain.com -o Output.txt`
	search engine dorking
	github dorking

	How to output to a file and remove any duplicates?

## Filtering for open sites
Doesn't return 400s
Returns 200s

## Finding open ports and other server
- https://www.shodan.io/
	- Search engine that indexes every device connected tot he internet
- nmap domain.com
- nmap ip address

## Script
1. Get txt file with list of subdomains
- amass
- sublist3r
- assetfinder
- GetAllUrls(GAU)
- Certificat Transparency Logs(CTL)
- subfinder
1. Remove any duplicates
`sort file.txt | uniq -u > file.txt`
1. Filter out any non loading subdomains
1. Organize subdomains
	- Redirects to
	- Login page
	- Unique page
	- Language site
	- API
	- 500s/bad request
	- 400s
	- Blocked/restricted
	- * any interesting sites


- Script that runs command -> regex to extract subdomains -> concat to file -> runs the next commands -> etc.
- Script which filters out any nonloading sub domains

- List tech stacks for each subdomain with wappalyzer
	- Different tech tacks communicating together may be areas with higher amounts of vulnerabilities
- List subdomains for attack vectors like XSS

- Script to list out site map from from lastmod first.
	- Good to look at older websites first
	- /sitemap.xml
	- /sitemap_index.xml