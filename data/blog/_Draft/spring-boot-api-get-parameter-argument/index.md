---
title: Spring Boot api 取得參數的幾種方式
summary: Spring Boot api 取得參數的幾種方式
date: 2024-03-18
tags: [ springboot ]
draft: true
---

![](./cover.webp)

```java
/**
*
 GET http://localhost:9100/query01?name=cash01
 *
*/
    @GetMapping("/query01")
    public String query01(String name)
    {
        System.out.println(name);
        return String.format("query string - %s", name);
    }

/**
*
 GET http://localhost:9100/query01?name=cash02

 @ RequestParam(name = "name", required = false)
 *
*/
    @GetMapping("/query02")
    public String query02(@RequestParam String name)
    {
        System.out.println(name);
        return String.format("query string - %s", name);
    }
/**
*
 GET http://localhost:9100/path/cash/get

 @ PathVariable(name = "name", required = false)
 *
*/
    @GetMapping("/path/{name}/get")
    public String path(@PathVariable String name)
    {
        System.out.println(name);
        return String.format("path - %s", name);
    }


/**
*
 GET http://localhost:9100/header
 name: cash

 @ RequestHeader(name = "name", required = false)
*/
    @GetMapping("/header")
    public String header(@RequestHeader String name)
    {
        System.out.println(name);
        return String.format("header - %s", name);
    }

/**
*
 GET http://localhost:9100/cookie
 Cookie: name=cash

 @ CookieValue(name = "name")
*/
    @GetMapping("/cookie")
    public String cookie(@CookieValue String name)
    {
        System.out.println(name);
        return String.format("cookie - %s", name);
    }

/**
*
 POST http://localhost:9100/form01
 Content-Type: application/x-www-form-urlencoded

 name = cash
*/
    @PostMapping("/form01")
    public String form01(String name)
    {
        System.out.println(name);
        return String.format("form01 - %s", name);
    }

/**
*
 POST http://localhost:9100/form02
 Content-Type: application/x-www-form-urlencoded

 name = cash
*/
    @PostMapping("/form02")
    public String form02(@RequestParam String name)
    {
        System.out.println(name);
        return String.format("form02 - %s", name);
    }

/**
*
 POST http://localhost:9100/form03
 Content-Type: application/x-www-form-urlencoded

 name = cash
*/
    @PostMapping("/form03")
    public String form03(Person person)
    {
        System.out.println(person);
        return String.format("form03 - %s", person);
    }

/**
*
 POST http://localhost:9100/form04
 Content-Type: application/x-www-form-urlencoded

 name = cash
*/
    @PostMapping("/form04")
    public String form04(@RequestParam Map<String, Object> map)
    {
        var name = map.get("name").toString();
        System.out.println(name);
        return String.format("form04 - %s", name);
    }

    /**
     *
     POST http://localhost:9100/form05
     Content-Type: application/x-www-form-urlencoded

     name = cash
     */
    @PostMapping("/form05")
    public String form05(@RequestParam(name = "name") Person person)
    {
        System.out.println(person);
        return String.format("form05 - %s", person);
    }

    /**
     *
     POST http://localhost:9100/form06
     Content-Type: application/x-www-form-urlencoded

     name = cash
     */
    @PostMapping("/form06")
    public String form06(@ModelAttribute(name = "name") String name)
    {
        System.out.println(name);
        return String.format("form06 - %s", name);
    }

/**
*
 POST http://localhost:9100/body01
 Content-Type: application/json

 {
 "name" : "cash"
 }
*/
    @PostMapping("/body01")
    public String body01(@RequestBody String name)
    {
        System.out.println(name);
        return String.format("body01 - %s", name);
    }

/**
*
 POST http://localhost:9100/body02
 Content-Type: application/json

 {
 "name" : "cash"
 }
*/
    @PostMapping("/body02")
    public String body02(@RequestBody Person person)
    {
        System.out.println(person);
        return String.format("body02 - %s", person);
    }

/**
*
 POST http://localhost:9100/body03
 Content-Type: application/json

 {
 "name" : "cash"
 }
*/
    @PostMapping("/body03")
    public String body03(@RequestBody Map<String, Object> map)
    {
        var name = map.get("name").toString();
        System.out.println(name);
        return String.format("body03 - %s", name);
    }

/**
*
 POST http://localhost:9100/file
 Content-Type: multipart/form-data; boundary=WebAppBoundary

 --WebAppBoundary
 Content-Disposition: form-data; name="file"; filename="file.txt"
 Content-Type: text/plain

 Name
 --WebAppBoundary

*/
    @PostMapping("/file")
    public String file(@RequestParam("file") MultipartFile uploadFile)
    {
        var originalFilename = uploadFile.getOriginalFilename();
        System.out.println(originalFilename);
        return String.format("file - %s", originalFilename);
    }
```


> 圖片來源：網路。若分享內容有侵害您的圖片版權，請來信告知，我們會及時加上版權信息，若是您反對使用，本著對版權人尊重的原則，會儘速移除相關內容。

> Photo by []() on [Unsplash]()



---

## 問題
## 原因
## 解法

## 參考連結