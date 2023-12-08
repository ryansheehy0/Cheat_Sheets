[Home](../README.md)

# Assetfinder
assetfinder is a terminal tool for finding sub domains. Sub domains are things other than "www" that go before the domain.

```
https://www.name.net
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
  - [Install Kali Linux tools](#install-kali-linux-tools)
  - [How to use](#how-to-use)
    - [Finding subdomains](#finding-subdomains)
    - [Searching multiple domains from a file](#searching-multiple-domains-from-a-file)
    - [Output to a file](#output-to-a-file)

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