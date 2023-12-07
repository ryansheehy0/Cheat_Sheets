# Assetfinder
assetfinder is a terminal tool for finding sub domains. Sub domains are things other than "www" that go before the domain.

https://www.name.net
[  ^   ][^] [ ^] [^]
   |     |    |   |
   |     |    | Top level Domain(TLD)
   |     | Domain
   | Sub-Domain
Protocol

| Common Sub-Domains | Description                                  |
|--------------------|----------------------------------------------|
| www                | Used to denote the default web page          |
| blog               | Used for hosting a blog from the main domain |
| shop               | Used for online store                        |
| api                | Dedicated to hosting APIs                    |
| app                | Used for histing web apps                    |
| beta               | beta features                                |

## Install Kali Linux tools
- Add `deb http://http.kali.org/kali kali-rolling main contrib non-free non-free-firmware` to /etc/apt/sources.list
- Run `sudo apt update`
  - If that doesn't work then run
  - `wget -O a "https://archive.kali.org/archive-key.asc" | apt-key add a`
  - Run `sudo apt update` again
- Run `sudo apt install assetfinder`


## How to use

### Finding subdomains
`assetfinder name.net`
- This also gets the connecting sites to the name.net

`assetfinder -subs-only name.net`
- This only gets the sub-domains of the name.net

### Searching multiple domains from a file
`cat domainfile.txt | assetfinder`

### Output to a file
`assetfinder name.net > outputfile.txt`