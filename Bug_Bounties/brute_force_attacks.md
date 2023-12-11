[Home](./README.md)

# Brute Force Attacks

**Brute force attacks** are attacks where an attacker tries all possible combinations of usernames and passwords until the correct one is found.

**Dictionary attacks** are attacks where an attacker tries a pre-defined set of usernames and passwords until the correct one is found.

Often it isn't practical to do brute force attack and that's why dictionary attacks are used instead.

## Table of Contents

<!-- TOC -->

- [Brute Force Attacks](#brute-force-attacks)
  - [Table of Contents](#table-of-contents)
  - [Hydra](#hydra)
  - [Wpscan](#wpscan)

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