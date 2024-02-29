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

# Path Traversal/Directory Traversal
Path traversal attacks happen when the user can input file paths into parameters and retrieve sensitive files by doing so.

Ex: An application makes a request from the server `GET /image?filename=218.png` or loads an image `<img src="/loadImage?filename=218.png">`

If the application doesn't parse the filename correctly you would navigate the server's directories by changing the parameter.

Ex: `GET /image?filename=./file`

Since you don't know what directory the server is checking for you can continually try to navigate up the directories and checking if your file is located there.

Ex: `GET /image?filename=../file`, `GET /image?filename=../../file`, `GET /image?filename=../../../file`, etc.

## Different ways of getting around directory parsing
- Use direct filepath.
	- Ex: `/file`
- `....//` or `....\/` instead of the usual `../`
- Use url decoding
	- `%2f` instead of `/`
	- `%5c` instead of `\`
	- `%252f` outputs `%2f`
	- `%255c` outputs `%5c`
	- `%c0%af` can output `/` depending upon the encoding used

## What files are common
- /etc/passwd
	- passwd contains details of the users registered on the server
- /etc/shadow
- /windows/win.ini
- .env

## Miscellaneous
- If the parameter requires a file path
	- Try: `./file%00.png`
- When making requests change the "Accept:" header to `*/*` to accept any file type