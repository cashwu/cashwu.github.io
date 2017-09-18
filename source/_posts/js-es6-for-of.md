---
title: JS ES6 for-of
tags:
  - js
categories: []
date: 2015-06-28 08:00:00
---


## ES5 for-in Array

```js
var list = ["a","b","c"];  
for(var index in list){  
    console.log(list[index]);
}

//result
//a
//b
//c
```

### ES6 for-of Array

```js
var list = ["a","b","c"];  
for(var val of list){  
    console.log(val);
}

//result
//a
//b
//c
```

### ES5 for-in String

```js
var str = "abc";  
for(var index in str){  
    console.log(str[index]);
}

//result
//a
//b
//c
```

### ES6 for-of String

```js
var str = "abc";  
for(var char of str){  
    console.log(char);
}

//result
//a
//b
//c
```
