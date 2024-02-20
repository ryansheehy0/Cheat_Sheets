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