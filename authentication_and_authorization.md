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

[Home](./README.md)

# Authentication And Authorization
**Authentication** is the process of logging in with a username and password.

**Authorization** is the process of making sure the user who logged in is the same user who is sending a request to the server.

```
     Client                           Server
       |
       +------(username and password)----->+
                                           | Authentication -> If username and hash(password + salt) matches what's in DB
Stored +<-(Generated Session ID and hash)--+                   then hash(Generated Session ID + Secret Key)
  on   |                                                       then store the user's session info
Client +--(request, Session ID, and hash)->+
                                           | Authorization -> If received hash == hash(Session ID + Secret Key) then authorized
       +<---(request info if authorized)---+
       |

```

In order for the server to make sure the Session ID isn't tamped with, the server combines its generated Session ID with its Secret Key and creates a hash.

If an attack were to try to change the Session ID, because they don't have the server's Secret Key, they cannot generate the right hash and thus they won't be authorized.

## Table of Contents
<!-- TOC -->

- [Authentication And Authorization](#authentication-and-authorization)
	- [Table of Contents](#table-of-contents)
	- [Cookies](#cookies)
	- [JSON Web TokensJWTs](#json-web-tokensjwts)
		- [Using JWTs on the Server](#using-jwts-on-the-server)
		- [Using JWTs on the Client](#using-jwts-on-the-client)

<!-- /TOC -->

Express Sessions

## [Cookies](#table-of-contents)
Cookies are just a way for the client to store information that is then automatically sent back to the server upon requests.

This is useful for authorization because you don't have to manually send the session ID.

Sometimes cookies aren't preferable to local storage because the cookies are sent on every request, event requests that might not need it.

## [JSON Web Tokens(JWTs)](#table-of-contents)
JWT is only used for authorization.

With JWTs, instead of the server storing the user's session info, the JWT itself caries all the user's session information.

JWTs are often used with cookies.

When the JWT is sent to the client it is encoded(Not encrypted) with base64. It is encoded in order to
- removes the "s, ?s, and other stuff that might accidentally break out of some input
  - Ex: It can be easily sent in the url path parameter.
    - https://website.com/eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ.SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

A JWT has 3 parts
- Header
  - metadata about the token. Describes what is the token.
```
// Encoded
eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9

// Decoded
{
  "alg": "HS256",
  "typ": "JWT"
}
```

- Payload
  - Data about the user and can be access on the front end and the back end
```
// Encoded
eyJzdWIiOiIxMjM0NTY3ODkwIiwibmFtZSI6IkpvaG4gRG9lIiwiaWF0IjoxNTE2MjM5MDIyfQ

// Decoded
{
  "sub": "1234567890",
  "name": "John Doe",
  "iat": 1516239022
}
```

- Signature
  - The signature is the hash which prevent data tampering
```
// Encoded
SflKxwRJSMeKKF2QT4fwpMeJf36POk6yJV_adQssw5c

// Decoded
HMACSHA256(
  base64UrlEncode(header) + "." +
  base64UrlEncode(payload),
  your-256-bit-secret
)
```

### [Using JWTs on the Server](#table-of-contents)
`npm install jsonwebtoken`

```javascript
const jwt = require("jsonwebtoken")

const secretKey = "This is the secret key that's kept secret on the server." // Make environment variable
const expiration = "2h" // The time the JWT stays valid for

function signJWT(payloadObj){ // This creates a new token
  return jwt.sign(payloadObj, secretKey, { expiresIn: expiration })
}

function verifyJWT(token){ // Sees if the token is valid
  try{
      // If the jwt is valid it will return the decodedPayload
    const decodedPayload = jwt.verify(token, secretKey, { maxAge: expiration /*Sees if the JWT has expired*/})
  }catch(error){
    // Token is invalid
    console.error(error)
  }
}

module.exports = createJWT
```

### [Using JWTs on the Client](#table-of-contents)

```javascript

```

client side
npm install jwt-decode

client/utils/auth.js
this.getToken