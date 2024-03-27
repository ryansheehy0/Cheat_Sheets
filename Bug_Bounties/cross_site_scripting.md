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
Cross site scripting(XSS) allows an attacker to get a victim to run malicious code on their browser while looking like it came from a legitimate source.

There are 2 type of XSS attacks.
- Through URL parameters
	- When a victim is sent a malicious URL, they may click on it because the base domain comes from a legitimate source.
		- **Reflected XSS**: Server uses the URL parameter to change the DOM.
		- **DOM-Based XSS**: Client uses the URL parameter to change the DOM.
- Through the database
	- **Stored XSS**: When the victim comes across malicious data stored in the database, that malicious data gets ran on their browser.
		- Ex: Posting a comment which other users can see.

## URL parameter XSS
- The URL parameter has to be used within the DOM.
- Form input sent via the URL and not the body can be used if it is inserted into the DOM.
- Fragment identifiers(`#`s in the URL) can be used by the client to change the DOM.
- Make sure to reload page after you change the URL parameter
- It may not show up visually in the page, but it is still inserted into the DOM.

Ex:
```
The URL
	https://insecure-website.com/status?message=<script>/*+Bad+stuff+here...+*/</script>
	or
	https://insecure-website.com#<script>/*+Bad+stuff+here...+*/</script>
The html output
	<p>Status: <script>/* Bad stuff here... */</script></p>
```

### Common client side code that gets the URL parameters(DOM-Based XSS)
- document.URL
- window.location or window.location.search
- document.location or document.location.search

Regex search: `(document|window)\.(.*\.)*(location|URL)`

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

## Common XSS filters
- Filtering out tags
	- Test all the tag
- Filter out events
	- Test all the events
- Filtering out special characters
	- Test alternatives to special character

See [XXS Tests](./xss_tests.md)

Often times inputs are filtered to remove or replace certain characters. This usually means that that input isn't susceptible to XSS attacks, however the filter might not be set up correctly.

| Filtered symbol | Try instead                                      |
|-----------------|--------------------------------------------------|
| `"`s or `'`s    | `&quot;`, `&lpar;` and `&rpar;`, `%27`, or `%22` |
| `<`s            | `&lt;`, `%3C`, or `\x3c`                         |
| `>`s            | `&gt;`, `%3E`, or `\x3e`                         |
| `\`s            | `\\`                                             |
| `(`s and `)`s   |                                                  |
| `&`s            | `%26` , `&amp;`                                  |
| `%`s            |                                                  |
| `.`s            |                                                  |
| `=`s            |                                                  |

Sometimes you need to add `">` or `'>` in front of your attacks as an escape sequence.

- It is often times worth try to double URL encode you input.

## Solutions to XSS attacks
- Better filters preferably from a library which specializes in such a thing
- Instead of sending things through the URL, send them though the body.

## Checklist
URl Parameter XSS:
1. Put unique string in URL parameter: `NkgM41FlLR`
2. Find a URL parameter that puts its output to the DOM.
	- Do ctrl+f in inspect element DOM to check for hidden DOM elements that contain the parameter.
3. Search in client JS for code which gets the query parameter.
4. Filter in Burp Suit for any responses containing the unique string.
5. Test basic XSS attacks
6. Figure out which characters are being filtered out and test alternative representations of those characters.

Stored XSS:
1. Create 2 accounts and log in. One in private browser.
2. Attacking account posts XSS attack.
3. 2nd account checks the post to see if it runs.

## All tags