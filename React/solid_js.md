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

# Solid JS
Solid JS is a library similar to react to build user interfaces. It makes some simplification to react which makes it faster than.

- Compiler to optimize
- Faster running
- Easier to use
- Doesn't use a virtual dom so you can interact with dom elements directly

The only difference between createMemo and createEffect is that createMemo returns a value.

Ref type
	let canvasRef: HTMLCanvasElement

createEffect
	- Setting a signal in createEffect creates an infinite loop and therefore should be used.
		- You can use the on function inside createEffect function to prevent infinite loops
	- Only updates when signal updates
	- Only updates if it checks the signal before any returns

Ex:
```javascript
	createEffect(() => {
		const value1 = signal1()
		if(value1 === true) return
		const value2 = signal2()
			// If signal2 is updated and value1 is true, then the createEffect doesn't get run again
	})
```

Downsides of solid js
- to call with state/signal you need to add the ().
	- Makes it harder to go from variable to state/signal
- useEffect/createEffect you can't just list the dependencies like in react
- can't use prop dereferencing in the arguments