---
title: Hello World Node.js 
tags:
  - nodejs
categories: []
date: 2016-01-09 08:00:00
---

> using VSCode

1、using command line install TSD and TSD package 
```shell
$ npm install -g tsd // if not install tsd
$ tsd install node --save // install node tsd file and save in tsd.json
```
2、create `app.js` file 
```js
var http = require("http");

var httpServer = http.createServer(function (request, response) {

    response.writeHead(200, { "content-type" : "text/html" });
    response.write("<h1>Hello World</h1>");
    response.end();

});

httpServer.listen(1234);

console.log("Server running at 1234 port");  
```
3、press `F5` and choose `Node.js`, then VSCode will create `.vscode` folder and `launch.json` file

4、press `F5` again, then VSCode will in Debug mode

5、browse `localhost:1234`, you can see `Hello World`

![](./nodejs-hello-world/01.png)

6、press `Shift + F5`, leave Debug mode back normal mode