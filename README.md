#Butler Router

[BUTLER_ROUTER](https://www.npmjs.com/package/butler_router)

How to install:
in your app folder run
```bash
$ npm install butler_router --save 
```

The basics:
```js
var br = require('butler_router');

br.newRoute("sub.domain.io", 12001);                 //Send all trafic accsing http(s)://sub.domain.io to port 12001
br.newRoute("sub2.domain.io", 3002, '/', "http");    //Only send trafic accsing http://sub.domain.io to port 3002
br.newRoute("sub2.domain.io", 9000, "/peerjs");      //foward trafic accessing sub2.domain.io/peerjs to port 9000
br.newRoute("sub4.domain.io", 12002, '/', "https");  //Add this to the https routes only
```

This sets the key and cert options for the https server.
You must have these set if you want to run the https server.
```js
br.httpsOptions = {
  key: fs.readFileSync('/path/to/privkey.pem'),
  cert: fs.readFileSync('/path/to/cert1.pem')
};
```

Start the server(s)
You can start all 3 (http, https, & default page)
```js
br.start();
```

Extra Options!

By defaul an express app serves all non routed trafic a basic "hello world" message.
By default it runs on port 12000
```js
br.defaultPagePort = 12000; 
```

The default port for the http server. If you leave this the same you must run the app with sudo.
```js
br.httpPort = 80 
```

The default port for the https server. If you leave this the same you must run the app as sudo.
```js
br.httpsPort = 443 
```

the default host for proxies.
```js
br.localPath = "http://localhost"  
```

Start the servers individually
```js
br.startHttp();
br.startHttps();
br.startDefault();
```

ADVANCED
Each instance of the server MUST have its own name.
If duplicates are presents error will persist.
```js
var port = 3080;
var name = "http_server2";
var httpFilter = function(req, res) {
  //return false to stop the routing process
}
br.srartHttp(port, name, httpFilter)

var httpsPort2 = 3443;
var httpsOptions2 = {
 key: fs.readFileSync('/path/to/key2.pem');
 cert: fs.readFileSync('/path/to/cert2.pem');
} 
var httpsServerName2 = "https_server2";
br.startHttps(httpsOptions2, httpsPort2, httpsServerName2);
```
##ISSUES
GitHub(https://github.com/tyler-r-smith/butler_router)

## People
[Tyler R Smith](http://q1s.co)
<t@q1s.co>

## License
[MIT](LICENSE)
