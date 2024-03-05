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

# Insecure Direct Object References(IDOR)

So IDOR happens when you can change a user id to another user that you shouldn't have access to?

IDOR vulnerabilities are exposing a user's sensitive features without needing authorization.

In order to test for IDORs you need to create 2 different accounts. The attacker's account and the victim's account.
- It is important to not attack a legitimate user's account.

## Places to check
- Hidden field elements
- Cookies
- URL parameters
- HTTP requests
	- Headers
	- Parameters
	- Body

- Cookies
	- 0 or 1 user ids are sometimes admin
	- Login, get cookie info, logout, login into different account, paste in old cookie info. Check if the session has ended and the cookies associated with that session.
- Check URL parameters
	- Check if there is authentication for different requests
- Check json body or parameters of HTTP requests from the client to the server
	- Check if there is authentication for different requests
	- Check if there is a problem with the logic. Ex: Changing the price of something you are adding to cart
	- Check the response format and try to add different properties to the response
- Logout, back button, and still authenticated/logged in


	- Check HTML and CSS source code
		- Hidden HTML Elements
		- Comments with sensitive information
		- URLs in the CSS
	- Check if any urls have any parameters
	- Check if there is any information in the cookies
	- Check for any unused CNAMEs