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

# Cross Site Request Forgery(CSRF)

Steps for CSRFs:
1. Victim logs into Site A and gets a session cookie.
1. While the user is still logged into Site A, they visit the attacker's websites(Site B).
1. Site B sends a malicious request to Site A.
1. The browser will automatically add Site A's session cookie to the malicious request and thus Site A accepts the malicious request.

## Things required for CSRFs
1. **Malicious action**: An action that the attacker would want to perform as another user.
1. **Cookie based session handling**: The server relies solely on the cookie session to identify the user who made the request.
1. **Predictable arguments**: The request doesn't contain any arguments that an attacker doesn't know or can't guess.

Ex:
```
POST /email/change HTTP/1.1
Host: vulnerable-website.com
Content-Type: application/x-www-form-urlencoded
Content-Length: 30
Cookie: session=yvthwsztyeQkAPzeQ5gHgTvlyxHfsAfE

email=wiener@normal-user.com
```
- This meats the 2 requirements.

Often times the malicious request is sent to Site A through a hidden html form.
```html
<html>
    <body>
        <form action="https://vulnerable-website.com/email/change" method="POST">
            <input type="hidden" name="email" value="pwned@evil-user.net" />
						<button type="submit">CSRF attack</button>
        </form>
        <script>
						// If you want to automatically submit the form.
            	//document.forms[0].submit();
        </script>
    </body>
</html>
```
- You can only perform CSRFs through form and not through fetch.
	- fetch requires cors(cross origin resource sharing) which doesn't allow cross domain cookies from being automatically added to the request.
	- form uses navigate which does automatically add cross domain cookies.
	- This is set through the Sec-Fetch-Mode: header.

## Why cookie over localstorage
Cookies are accessible to any site in the same browser instance. Localstorage is only accessible to the site itself.
Thus allows cookies to be susceptible to CSRFs and not localstorage. So why are sessions commonly stored in cookies and not localstorage?

localstorage/sessionstorage:
- Divided between HTTP and HTTPS
- Divided between subdomains

cookies
- Accessible to both HTTP and HTTPS
	- Unless it has the secure attribute
- Read by javascript 

https://stackoverflow.com/questions/35291573/csrf-protection-with-json-web-tokens/

Cookies are marked with a domain. When a request is made to a server, the browser will send all cookies with the matching domain regardless of .

Cookies are sent via the headers.

There are such things as same site cookies.

## Purpose of nonces
	- nonce is used to prevent CSRFs
To stop these attacks you would use a nonce(number only once).
	- Changes per user and changes every time the server sends back the get.
