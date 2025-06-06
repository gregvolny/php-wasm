# [![seanmorris/php-cgi-wasm](https://github.com/seanmorris/php-wasm/blob/master/docs/sean-icon.png)](https://github.com/seanmorris/php-wasm) php-cgi-wasm

find php-cgi-wasm on [npm](https://npmjs.com/package/php-cgi-wasm)

_The CGI Counterpart to [php-wasm](https://npmjs.com/package/php-wasm)._

This package encompasses the CGI-specific build artifacts of php-wasm. The goal of this part of the project is to provide a version of PHP that more closely resembles the environment facilitated by PHP when running under web servers like Apache and nginx. This is achieved by building a binary artifact of PHP-CGI, rather than PHP-CLI to Web Assembly. The resulting WASM binary can then be run under nodejs with express, in a webpage, or inside a service worker.

## Example Service Worker

```javascript
import { PhpCgiWorker } from "php-cgi-wasm/PhpCgiWorker";

// Spawn the PHP-CGI binary
const php = new PhpCgi({
	prefix: '/php-wasm'
	, docroot: '/persist/www'
	, types: {
		jpeg: 'image/jpeg'
		, jpg: 'image/jpeg'
		, gif: 'image/gif'
		, png: 'image/png'
		, svg: 'image/svg+xml'
	}
});

// Set up the event handlers
self.addEventListener('install',  event => php.handleInstallEvent(event));
self.addEventListener('activate', event => php.handleActivateEvent(event));
self.addEventListener('fetch',    event => php.handleFetchEvent(event));
self.addEventListener('message',  event => php.handleMessageEvent(event));
```
