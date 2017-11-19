# 配置 HTTPS

## 申请证书

可以在阿里云、腾讯云、百度云申请免费的 DV SSL 证书，该证书申请简便，缺点是仅支持 1 个域名。

## 代码

```javascript
const https = require('https');
const fs = require('fs');

const options = {
	pfx: fs.readFileSync('cert/cert.pfx'),
	passphrase: 'password'
};

https.createServer(options, (req, res) => {
	if (req.headers.host.indexOf('.nodejs.top') > 0) {
		res.writeHead(301, { 'Location': 'https://nodejs.top' });
		res.end();
	} else {
		res.writeHead(200, { 'Content-Type': 'text/html' });
		res.write('<h1>Node.js</h1>');
		res.end('<p>Hello World!</p>');
	}
}).listen(443);
```