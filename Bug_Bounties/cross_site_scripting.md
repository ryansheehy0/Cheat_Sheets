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

# Cross Site Scripting(XSS)
Cross site scripting(XSS) allows an attacker to send another user a URL or data which then executes the attacker's javascript code on the victim's browser and thus have access to the victims local storage, cookies, and any other functionally the user can do.

The reason XSS is bad is because an attacker can look like the legitimate site and yet execute their attack in the victim's browser.

Often times in order to find XSS vulnerabilities your payload would be `alert()` or `print()`. `print()` is recommended because it works on more browsers. This gives a very clear way of identify when a vulnerability is found.

`alert(document.domain)`
`alert(window.origin)`

There are 2 main types of XSS
- Reflected XSS/DOM-based XSS: Through the URL
- Stored XSS: Through the database

## Reflected XSS/DOM-Based XSS
A URL parameter or fragment identifier(#s to html headers) can execute JS code.

**Reflected XSS** sends a request to the server and the server sends back html with the user's input in it.

**DOM-based XSS** happen when the clients's code directly adds the user input into the html of the page.

Ex:
```
The URL
	https://insecure-website.com/status?message=<script>/*+Bad+stuff+here...+*/</script>
	or
	https://insecure-website.com#<script>/*+Bad+stuff+here...+*/</script>
The html output
	<p>Status: <script>/* Bad stuff here... */</script></p>
```

You probably want to reload the page after the XSS input.

## Stored XSS
The attacker inputs their JS code into the database and then the database gives it to a victim. Ex: Posting a comment which other users can see. If that comment contains js code and the site is vulnerable to XSS then the attacker's js code gets ran whenever a victim gets the data from the database.

## Common attacks
- `<script>print()</script>`
- `<img src=x onerror="print()"/>`
- `<a href="javascript:print()">`
- `<img src onerror=print()>`