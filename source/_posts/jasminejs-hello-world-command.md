---
title: Hello World Jasmine.js (using command line)
tags:
  - jasminejs
  - js
categories: []
date: 2016-01-11 08:00:00
---

> using VSCode
>
> reference before article Hello World Jasmine.js

1、install jasmine and jasmine tsd in command line
```shell
$ npm install -g jasmine // if not install jasmine
$ jasmine init // init jasmine in /spec/support/jasmine.json

$ npm install -g tsd // if not install tsd  
$ tsd install jasmine --save // install node tsd file and save in tsd.json  
```
2、create `hello.js` file in `new src` folder
```js
Object.prototype.SayHello = function(){  
    return "Hello World !";
}    
```
4.create `hello.spec.js` file in spec folder
```js
require("../src/hello.js");

describe("Hello world Test", function(){

   it("says hello", function(){
        expect(SayHello()).toEqual("Hello World !");
   })

});
```
5.using command line run Jasmine Test, you can see `0 failures`

```shell
$ jasmine
```

![](./jasminejs-hello-world-command/01.png)

6.if modify `hello.js`

```js
Object.prototype.SayHello = function(){  
    return "Hello World 123";
}   
```

7.rerun Jasmine Test, you can see 1 failures

```shell
$ jasmine
```

![](./jasminejs-hello-world-command/02.png)