[Home](../README.md)

# Insecure Direct Object References(IDOR)

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

You can test with BURP
	- Intercept any HTTP request made from the client to the server
	- How to set up BURP