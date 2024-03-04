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

Need to research Blind SSRF vulnerabilities on portswigger.net
Sometimes the server checks for headers for links.

# Server Side Request Forgery(SSRF)

SSRF happens when a server accepts arguments in the form of URLs or URL paths which can allow an attacker to trick the server into loading URLs that it normally wouldn't want to.
- Cause the server to send back information from other internal servers
- Cause the server to connect to an attacker's eternal websites

Ex: A website accepts a URL as an argument in its body
```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://stock.weliketoshop.net:8080/product/stock/check%3FproductId%3D6%26storeId%3D1
```

The URL argument can be modified to point to `/admin`, which gives access to the admin page for the attack.
```
POST /product/stock HTTP/1.0
Content-Type: application/x-www-form-urlencoded
Content-Length: 118

stockApi=http://localhost/admin
```

The attacker wouldn't normally have access to this page, but because the server itself goes to that path, it does have access and then sends the page to the client/attacker.
- You can often go to certain pages, but you won't be given access. This is a way to get around that.
- It is a way to get around restricted sites.

## Common domains
- `localhost`
- loopback addresses: `127.0.0.1` - `127.255.255.255`
- private addresses: `10.0.0.0` - `10.255.255.255.255`, `172.16.0.0` - `172.31.255.255`, and `192.168.0.0` - `192.168.255.255`
	- You have to check each of these individually because you don't know what other devices are on their private network

## Get around common SSRF filters
- Alternatives to `127.0.0.1` like `2130706433`(decimal representation), `017700000001`(octal representation), or `127.1`.
- Register a domain name that resolves to `127.0.0.1`
	- Use A record
	- Try changing protocols from `https` to `http`
- URL encoding or case variation
	- It is often worth trying to double encode special characters. Like `#` double encoded as `%2523` or `:` as `%253A`

Sometime SSRF filter only allow URLs that contain or start with permitted values. Here are some tips to get around that:
- Using the @ symbol so the username or password can bypass the filter, but not change the actual domain. This takes the format of `username:password@domain`
	- Ex: `https://permitted-value:fakepassword@127.0.0.1` or `https://fakeusername:permitted-value@127.0.0.1`
	- Sometimes arguments take in URL paths and concatenate those paths onto the `localhost`
		- Ex: `http://localhost:80 + parameter` or `http://localhost + parameter`
		- parameter = `@197.168.0.12/admin` or `:fakepassword@197.168.0.12/admin`
		- Output = `http://localhost:80@197.168.0.12/admin` or `http://localhost:fakepassword@197.168.0.12/admin`
- Using the # symbol so the permitted value is in the fragment identifier and thus passes the filter, but doesn't change the domain.
	- Ex: `https://127.0.0.1#permitted-value`
	- This works if the URL needs to contain one of the permitted values, but doesn't need to start with it.
- Using sub-domains so the permitted-value is in the subdomain, but doesn't effect the actual domain being searched.
	- Ex: `https://permitted-value.127.0.0.1`
- You can combine each of these approaches
	- Ex: `http://localhost%2523username@stock.weliketoshop.net/admin`
