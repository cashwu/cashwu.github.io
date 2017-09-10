---
title: Node.js Modules
tags:
  - nodejs
categories: []
date: 2016-01-17 08:00:00
---

> using VSCode
>
> reference before article Hello World Node.js

1.create a `server.js` file, move `app.js` code to `server.js` and modify

```js
var http = require("http");

function start(){

    function onRequest(request, response) {

        response.writeHead(200, { "content-type" : "text/html" });
        response.write("<h1>Hello World</h1>");
        response.end();

    };

    http.createServer(onRequest).listen(1234);

    console.log("Server running at 1234 port");      
}

exports.start = start;  
```

2.modify `app.js`

```js
var server = require("./server");

server.start();  
```

3.press `F5`

4.browse `localhost:1234`, you can see Hello World same before