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

# Cross Origin Resource Sharing(CORS)

- Enables controlled access to resources located outside of a given domain
- Adds flexibility to same origin policy
- CORS is not a protection against CSRFs
	- Why? Is that because of forms?

Same origin policy(SOP)
- Allows a website to get and give data from its own URL, but blocks things from external URLs unless certain conditions are met.
- Only applies to scripts running in the browser and doesn't include servers of form inputs.
- In order to get around SOP the URL you are making a request to has to change their CORS settings.
	- The URL has control over who can access its resources and under what conditions
	- **Access-Control-Allow-Origin(ACAO)**
		- Specifies which origins have access. `*` is used to say all origins or you can specify
		- What about an array of origins?
		- Can you have an array of excluded origins?
	- **Across-Control-Allow-Methods(ACAM)**
		- Specifies which HTTP methods are allowed(GET, POST, PUT, etc)
	- **Access-Control-Allow-Headers(ACAH)**
		- Specifies which headers can be used for the request
	- **Access-Control-Allow-Credentials(ACAC)**
		- Can requests include cookies, HTTP authentication, and client-side SSL certificates
			- Can be either true or false
			- What is HTTP authentication and why would client-side SSL certificates matter? Wouldn't it not work if those weren't sent when using HTTPS?
	- **Access-Control-Expose-Headers(ACEH)**
		- Which headers can be exposed in the response.
		- How is this different from Access-Control-Allow-Headers?
			- I think allow means which headers are allowed in the request while expose is for the response.
	- **Access-Control-Max-Age(ACMA)**
		- I don't know
- How is a fetch request different from a form request?
- How can you see another URLs CORS settings?

## Misconfigurations of CORS settings
- Change or add Origin header to a random URL
	- If it ACAO accepts it then it most likely accepts all URLs
	- If it also sets ACAC to true then this could be a CSRF vulnerability that can use fetch or XMLHttpRequest.


- Overly lenient to ensure everything works.
- If ACAO is set to allow any domains you can run this code to do a CSRF attack
```javascript
let req = new XMLHttpRequest()
req.open('GET', 'https://vulnerable-website.com/sensitive-victim-data')
req.withCredentials = true
req.onload = () => {
	console.log(req.response)
}
req.send()
```