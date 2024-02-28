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

# Assetfinder
assetfinder is a terminal tool for finding sub domains. Sub domains are things other than "www" that go before the domain.

## Table of Contents
<!-- TOC -->

- [Assetfinder](#assetfinder)
	- [Table of Contents](#table-of-contents)
	- [Install Kali Linux tools](#install-kali-linux-tools)
	- [How to use](#how-to-use)
		- [Finding subdomains](#finding-subdomains)
		- [Searching multiple domains from a file](#searching-multiple-domains-from-a-file)
		- [Output to a file](#output-to-a-file)
	- [Finding different paths](#finding-different-paths)

<!-- /TOC -->

## [Install Kali Linux tools](#table-of-contents)
- Add `deb http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware` to /etc/apt/sources.list
- Run `sudo apt update`
  - If that doesn't work then run
  - `wget -O a "https://archive.kali.org/archive-key.asc" | apt-key add a`
  - Run `sudo apt update` again
- Run `sudo apt install assetfinder`

## [How to use](#table-of-contents)

### [Finding subdomains](#table-of-contents)
`assetfinder name.net`
- This also gets the connecting sites to the name.net

`assetfinder -subs-only name.net`
- This only gets the sub-domains of the name.net

### [Searching multiple domains from a file](#table-of-contents)
`cat domainfile.txt | assetfinder`

### [Output to a file](#table-of-contents)
`assetfinder name.net > outputfile.txt`

## [Finding different paths](#table-of-contents)
- https://www.name.net/robots.txt
  - robots.txt is a text file which tells web crawlers which parts of the site should not be crawled or should be crawled with certain restrictions.