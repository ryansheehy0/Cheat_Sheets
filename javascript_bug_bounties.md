[Home](./README.md)

# Javascript Bug Bounties

## Table of Contents

<!-- TOC -->

- [Javascript Bug Bounties](#javascript-bug-bounties)
  - [Table of Contents](#table-of-contents)
  - [Links](#links)
  - [How to choose a target?](#how-to-choose-a-target)
  - [How to find the source code?](#how-to-find-the-source-code)
  - [Things to keep in mind](#things-to-keep-in-mind)
  - [What qualifies as a vulnerability](#what-qualifies-as-a-vulnerability)
  - [Static Analysis Security TestingSAST tools](#static-analysis-security-testingsast-tools)
  - [Useful Terms](#useful-terms)
  - [SQL Injection](#sql-injection)
  - [Cross site scriptingXSS](#cross-site-scriptingxss)
  - [Authentication and Authorizations attacks](#authentication-and-authorizations-attacks)
  - [File upload vulnerabilities](#file-upload-vulnerabilities)
  - [Server side request forgeriesSSRF](#server-side-request-forgeriesssrf)
  - [Cross-Site Request ForgeryCSRF](#cross-site-request-forgerycsrf)
  - [Insecure Deserialization](#insecure-deserialization)
  - [Insecure Direct Object ReferencesIDOR](#insecure-direct-object-referencesidor)
  - [Submitting a vulnerability](#submitting-a-vulnerability)

<!-- /TOC -->

- Lack of input validation
- Lack of output encoding
- Midding access control
- Weak regex checks
- Server side request forgeries
- Open redirects

## [Links](#table-of-contents)
- https://www.hackerone.com/
- 

## [How to choose a target?](#table-of-contents)
- Offer bug bounties
- Good candidates
  - Sufficiently complex application

## [How to find the source code?](#table-of-contents)
  - Look at the client side code
  - Reverse engineer the source code
  - Github, pastebin, wayback machine

## [Things to keep in mind](#table-of-contents)
- Understand the application and what the application is trying to do before looking for bugs
- What are the different permissions of each user
- How are inputs and outputs being authenticated

## [What qualifies as a vulnerability](#table-of-contents)
- Getting information you aren't supposed to see

## [Static Analysis Security Testing(SAST) tools](#table-of-contents)
  - Can have false positives or false negatives.
    - Need to always manually check

## [Useful Terms](#table-of-contents)

| Term                       | Description |
|----------------------------|-------------|
| Privilege escalation       |             |
| Remote Code Execution(RCE) |             |
| I/O doors                  |             |
| Missing access controls    |             |

**0 day exploit** is an exploit that the target has had zero days of knowing about that vulnerability.

## [SQL Injection](#table-of-contents)
## [Cross site scripting(XSS)](#table-of-contents)
## [Authentication and Authorizations attacks](#table-of-contents)
## [File upload vulnerabilities](#table-of-contents)
## [Server side request forgeries(SSRF)](#table-of-contents)
## [Cross-Site Request Forgery(CSRF)](#table-of-contents)
## [Insecure Deserialization](#table-of-contents)
## [Insecure Direct Object References(IDOR)](#table-of-contents)

JWT attacks
BOLA broken objects level authorization

## [Submitting a vulnerability](#table-of-contents)
- Screenshots
  - Highlighting the important points
- Step by step guide to replicate attack
- If you have the knowledge then recommendations on how to solve the problem.