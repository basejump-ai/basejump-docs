# Cross-Origin Communication

**Embedding the Basejump chat UI involves cross-origin (cross-domain) communication between your application and Basejump servers.** To enable this integration, you must configure your application to permit iframes from `app.basejump.ai`.

Set your `X-Frame-Options` HTTP response header to allow embedding from Basejump by including the following value:

```html ~Example X-Frame-Options:~
X-Frame-Options: ALLOW-FROM https://app.basejump.ai
```

The embed code loads external scripts and stylesheets from `cdn.basejump.ai` and displays an iframe that communicates with `app.basejump.ai` via HTTP requests and websockets. Your Content Security Policy (CSP) must explicitly allow these domains for scripts, styles, images, frames, and connections to ensure the embed works properly:

```html ~Example CSP:~
Content-Security-Policy: 
script-src 'self' https://app.basejump.ai https://cdn.basejump.ai; 
style-src 'self' https://app.basejump.ai https://cdn.basejump.ai; 
img-src 'self' https://app.basejump.ai https://cdn.basejump.ai; 
connect-src 'self' https://app.basejump.ai; 
frame-src 'self' https://app.basejump.ai
```