---
title: Node.js - Url Routing
summary: Node.js - Url Routing
date: 2016-01-18 19:50:59.609+08:00
tags: [ nodejs ]
draft: false
---

> using VSCode
> reference before article Node.js Modules

1、modify `server.js` 

```js
var http = require("http");  
var url = require("url");

// inject the route module in app.js, not direct using
function start(route){

    function onRequest(request, response) {
        // using url module get url pathname;
        var pathname = url.parse(request.url).pathname;
        console.log("Request for " + pathname + " received");
        console.log("Request url: " + request.url);
        // let route handle pathname
        route(pathname); 

        response.writeHead(200, { "content-type" : "text/html" });
        response.write("<h1>Hello World</h1>");
        response.end();

    };

    http.createServer(onRequest).listen(1234);

    console.log("Server running at 1234 port");      
}

exports.start = start;  
```

2、create `router.js` file

```js
function route(pathname){  
    //you can handle url path in here
    console.log("Route this request : " + pathname);
}

exports.route = route;  
```

3、modify `app.js` 

```js
var server = require("./server");  
var router = require("./router");

// inject router in server
server.start(router.route);  
```

4、press `F5`

5、browse `localhost:1234`, you can see `Hello World` and the log in VSCode debug console window

![](/static/images/404.webp)