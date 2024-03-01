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

Often times in order to find XSS vulnerabilities your payload would be `alert()` or `print()`. `print()` is recommended because it works on more browsers.

There are 2 main types of XSS
- Reflected XSS: Through the URL
- Stored XSS: Through the database

## Reflected XSS
A URL parameter can execute JS code.

Ex:
```
The URL
	https://insecure-website.com/status?message=<script>/*+Bad+stuff+here...+*/</script>
The html output
	<p>Status: <script>/* Bad stuff here... */</script></p>
```

## Stored XSS
The attacker inputs their JS code into the database and then the database gives it to a victim. Ex: Posting a comment which other users can see. If that comment contains js code and the site is vulnerable to XSS then the attacker's js code get ran whenever 

## Common attacks
- `





```javascript
<img src= onerror="alert('1')"/>
// If img is blocked
<imG />
// If / is blocked
<button onclick="alert('1')">click
```