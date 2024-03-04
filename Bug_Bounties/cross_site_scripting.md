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
https://github.com/PortSwigger/xss-validator
Uploading .html file
```
%PDF-1.4
%Ã¤Ã¼Ã¶Ã
2 0 obj
<</Length 3 0 R/Filter/FlateDecode>>
stream
x=Ë
1E÷ù»v¶é´0è~ àø
R
R<h1>This is NOT a PDF!</h1> <img src=x onerror=alert(document.cookie)>
```

# Cross Site Scripting(XSS)
Cross site scripting(XSS) allows an attacker to send another user a URL or data which then executes the attacker's javascript code on the victim's browser and thus have access to the victims local storage, cookies, and any other functionally the user can do.

The reason XSS is bad is because an attacker can look like the legitimate site and yet execute their attack in the victim's browser.

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

### Common sinks

Different DOM-Based sinks. Do a ctrl+f:
- document.write
- document.domain
- window.location.search
- eval()
- innerHTML
- outerHTML
- insertAdjacent
- insertBefore
- insertAfter
- onevent

JQuery sinks:
- add(), after(), append(), animate(), insertAfter(), insertBefore(), before(), html(), prepend(), replaceAll(), replaceWith(), wrap(), wrapInner(), wrapAll(), has(), constructor(), init(), index(), jQuery.parseHTML(), $.parseHTML()

## Stored XSS
The attacker inputs their JS code into the database and then the database gives it to a victim. Ex: Posting a comment which other users can see. If that comment contains js code and the site is vulnerable to XSS then the attacker's js code gets ran whenever a victim gets the data from the database.

## Common attacks
- `<script>print()</script>`
- `<img src onerror=print()>`
- `<a href="javascript:print()">`

[Good payload list](https://github.com/payloadbox/xss-payload-list)

## Common payloads to try
- `print()`
- `alert()`
- `confirm()`
- `prompt()`
- `console.log()`

Often times it is also good to check if you can access this information
- `document.domain`
- `window.origin`
- `document.cookies`

## Get around common XSS filters
Often times inputs are filtered to remove or replace certain characters. This usually means that that input isn't susceptible to XSS attacks, however the filter might not be set up correctly.

| Filtered symbol | Try instead                               |
|-----------------|-------------------------------------------|
| `"`s or `'`s    | `&quot;`, `&lpar;` and `&rpar;`, `%27`, or `%22` |
| `<`s            | `&lt;`, `%3C`, or `\x3c`                  |
| `>`s            | `&gt;`, `%3E`, or `\x3e`                  |
| `\`s            | `\\`                                      |
| `(`s and `)`s   |                                           |
| `&`s            |  `%26` , `&amp;`                                        |
| `%`s            |                                           |
| `.`s            |                                           |
| `=`s            |                                           |

Sometimes you need to add `">` or `'>` in front of your attacks as an escape sequence.

- It is often times worth try to double URL encode you input.
- Try URL encoding ascii characters with the hex representation fo the ascii `%hex`
	- You can try to double URL encode this as well

## Solutions to XSS attacks
- Better filters preferably from a library which specializes in such a thing
- Instead of sending things through the URL, send them though the body.

## Checklist
1. Check for common attacks in the browser
	- Change the payload
1. If not working, check common symbol filters in burp suite repeater and see if it's in the response.
	- Filter in burp suite proxy -> HTTP History for NkgM41FlLR then send to repeater
	- NkgM41FlLR
1. If nothing else works, execute an automated attack with burp suite intruder with a payload list
