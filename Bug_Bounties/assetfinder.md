[Home](../README.md)

# Assetfinder
assetfinder is a terminal tool for finding sub domains. Sub domains are things other than "www" that go before the domain.

```
https://www.name.net/path
[  ^   ][^] [ ^] [^]
   |     |    |   |
   |     |    | Top level Domain(TLD)
   |     | Domain
   | Sub-Domain
Protocol
```

| Common Sub-Domains | Description                                  |
|--------------------|----------------------------------------------|
| www                | Used to denote the default web page          |
| blog               | Used for hosting a blog from the main domain |
| shop               | Used for online store                        |
| api                | Dedicated to hosting APIs                    |
| app                | Used for histing web apps                    |
| beta               | beta features                                |

## Table of Contents
<!-- TOC -->

- [Assetfinder](#assetfinder)
  - [Table of Contents](#table-of-contents)
  - [](#)
  - [](#)
    - [](#)
    - [](#)
    - [](#)
  - [](#)

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