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

# Server Side Request Forgery(SSRF)

- Allows an attacker to control the server and make it request to unintended locations.
- Cause the server to send back information from other internal servers
- Cause the server to connect to an eternal system

- Input `127.0.0.1` or `localhost`

- Server accepts URL arguments(in body or URL parms) in requests which can be modified to point to a localhost or 127.0.0.1 URL
- http://localhost/admin
	- The attacker can access that /admin path, but they do not have access. But if the server itself goes to that path it would have access.
	- It is a way to get around restricted sites.
- It is also worth checking any private ip addresses. 10.0.0.0 - 10.255.255.255.255, 172.16.0.0 - 172.31.255.255, and 192.168.0.0 - 192.168.255.255
- Sometimes URLs are filtered to remove any potential SSRFs. You can try
	- Alternatives to `127.0.0.1` like `2130706433`(decimal representation), `017700000001`(octal representation), or `127.1`.
	- Register a domain name that resolves to 127.0.0.1 like `spoofed.burpcollaborator.net`
	- URL encoding or case variation
	- URL which redirects to the target URl. Try changing protocols from https to http
	- Use XSS tips to bypass any SSRF filters


Sometime SSRF filter only allow URLs that contain or start with permitted values. Here are some tips to get around this.
- https://permitted-value:fakepassword@127.0.0.1 or https://fakepassword:permitted-value@127.0.0.1
	- Since the server isn't handling the username:password it gets ignored, but it still passes the filter.
- https://127.0.0.1#permitted-value
	- This works if the URL needs to contain one of the permitted values
- https://permitted-value.127.0.0.1
- Try double encoding URLs
	- Try to double encode # like `%2523`
	- Ex: `http://localhost%2523username@stock.weliketoshop.net/admin`