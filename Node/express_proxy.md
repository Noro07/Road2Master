# 设置 express 的 proxy，在不同情况下转发到不同的 host

## 使用 http-proxy-middleware

```js
var express = require('express');
var proxy = require('http-proxy-middleware');

var app = express();

app.use(
  '/api',
  proxy({ target: 'http://www.example.org', changeOrigin: true })
);
app.listen(3000);

// http://localhost:3000/api/foo/bar -> http://www.example.org/api/foo/bar
```

如果不通的情况，可以添加以下元素

```js
app.use(
  "/amg",
  proxy({
    target: "http://localhost:8080",
    onProxyReq: restream,
    secure: false,
    logLevel: "debug",
    changeOrigin: true,
    pathRewrite: { "^/amg": "http://localhost:8080/amg" },
    headers: {
      Connection: "keep-alive"
    }
  })
);
```


## get 能通但是 post 收不到请求

<https://github.com/chimurai/http-proxy-middleware/issues/40>

解决方案 1:

修改顺序，将 proxy 的顺序放在 body-parser 的上面就可以避免被覆盖
You might want to change to order of the middlwares you are using.
Try moving the `http-proxy-middleware` above the`body-parser`

解决方案 2:
因为缺失 body，在这里补充

```js
// restream parsed body before proxying
var restream = function(proxyReq, req, res, options) {
  if (req.body) {
    let bodyData = JSON.stringify(req.body);
    // incase if content-type is application/x-www-form-urlencoded -> we need to change to application/json
    proxyReq.setHeader('Content-Type', 'application/json');
    proxyReq.setHeader('Content-Length', Buffer.byteLength(bodyData));
    // stream the content
    proxyReq.write(bodyData);
  }
};

var apiProxy = proxyMiddleware('/api', {
  target: 'https://xxx.xxx.xxx.xxx',
  onProxyReq: restream
});

var app = express();

app.use(bodyParser.json());
app.use(bodyParser.urlencoded());
app.use(apiProxy); // with restreaming
```

ref:
<https://github.com/chimurai/http-proxy-middleware>
