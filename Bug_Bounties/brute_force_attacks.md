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

[Home](./README.md)

# Brute Force Attacks

Just use Burp Suite Intruder
Select username and password


**Brute force attacks** are attacks where an attacker tries all possible combinations of usernames and passwords until the correct one is found.

**Dictionary attacks** are attacks where an attacker tries a pre-defined set of usernames and passwords until the correct one is found.

Often it isn't practical to do brute force attack and that's why dictionary attacks are used instead.

## Table of Contents

<!-- TOC -->

- [Brute Force Attacks](#brute-force-attacks)
	- [](#)
	- [Hydra is a tool for doing dictionary attacks on websites.](#hydra-is-a-tool-for-doing-dictionary-attacks-on-websites)
	- [](#)

<!-- /TOC -->

## [Hydra](#table-of-contents)
Hydra is a tool for doing dictionary attacks on websites.

If an http form prevents default and submits via javascript then hydra won't work.

`sudo hydra [-l Login|-L File] [-p PASS|-P File] [-u][-f][IP Address|Domain name] [-s Port] [Module] [url]:[form parameters]:[condition string]`

| Flags    | Description                                                  |
|----------|--------------------------------------------------------------|
| -l Login | Login name                                                   |
| -L File  | File of logins to use                                        |
| -p Pass  | Password to use                                              |
| -P File  | File of passwords to use                                     |
| -u       | Try every username for each password                         |
| -f       | Stop trying to find passwords once the first match is found. |
| Module   | A Module is a service to attack. Ex: http-post-form, mysql5, ssh, etc          |
| -s Port  | Different from the default port.                             |

| Port name                   | Default port |
|-----------------------------|--------------|
| FTP(File transfer protocol) | 21           |
| SSH(Secure shell)           | 22           |
| HTTP                        | 80           |
| HTTPS                       | 443          |

The **form parameters** are the parameters sent via the url when the form submits.

The **condition string** tells hydra when to stop trying passwords or to continue trying passwords.
  - If you want to define something when the login is successful use `:F=<`. This could be the login form itself.
  - If you want to define something when the login fails use `:`. This could be the error message when the login fails.

^USER^ is the username given by hydra.

^PASS^ is the password given by hydra.

Example:
```
// When condition string is when the login fails:
  sudo hydra -L ./SecLists/Usernames/top-usernames-shortlist.txt -P ./SecLists/Passwords/Leaked-Databases/rockyou-75.txt -u -f example.com http-post-form "/path:user=^USER^&password=^PASS^:Invalid credentials"
// When condition string is when the login was successful:
  sudo hydra -L ./SecLists/Usernames/top-usernames-shortlist.txt -P ./SecLists/Passwords/Leaked-Databases/rockyou-75.txt -u -f example.com http-post-form "/path:user=^USER^&password=^PASS^:F=<form name='login'"
```

## [Wpscan](#table-of-contents)