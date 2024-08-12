---
title: 在 js 裡面使用 Parse Server
description: 前面的文章已經把 Parse Server 架設在 Heroku 了，現在就來看怎麼在 js 裡面連接到 Parse Server 取得資料
date: 2018-12-24 09:23:12.376+08:00
slug: "js-parse-server"
tags: [ js , parse ]
---

前面的[文章](https://blog.cashwu.com/blog/heroku-parse-server)已經把 Parse Server 架設在 Heroku 了，現在就來看怎麼在 js 裡面連接到 Parse Server 取得資料

## Query

- 建立一個空白的 Html 檔案

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <title>Title</title>
</head>
<body>
    OK
</body>
</html>
```

- 引用 `parse.js`

> 這裡為了測試方便直接在頁面引用 `parse.js`，如果是在前端框架裡面使用請使用 `npm` 安裝

```html
<script src="//npmcdn.com/parse@2.1.0/dist/parse.js"></script>
```

- 初始化 Parse Server
	- `initialize` 第一個參數請傳入設定好的 `AppId`，第二個參數是 `javaScriptKey` 沒有設定的話可以不傳
	- `URL` 記得換成自己設定的

```html
<script>
    Parse.initialize('appid', 'unused');
    Parse.serverURL = 'https://cashparse.herokuapp.com/parse';
</script>
```

- 取得資料
	- `Query` 裡面傳的是 `classes` 的名稱
	- 可以用 find 來找到全部的資料

```html
<script>
    Parse.initialize('appid');
    Parse.serverURL = 'https://cashparse.herokuapp.com/parse';
	var query = new Parse.Query('GameScore');
	query.find().then(function(result){
		console.log(result);
	});
</script>
```

- 打開 console 就可以看到有兩筆資料

![](/images/404.webp)

- 可以使用之前[文章](https://blog.cashwu.com/blog/install-parse-server-dashboard)架設的 Dashboard 來比對
	- 左邊紅色框起來的部份就是 `classes`

![](/images/404.webp)

> 其它詳細的 API 用法請參考[官方 SDK](https://docs.parseplatform.org/js/guide/#queries)

## Live Query

- 如果要作到像 SignalR 一樣即時拿到推送的資料的話，就要使用 `Live Query`

- 修改 js，Query 裡面要換成有支援 `Live Query` 的 classes
	- 必須要使用 `subscribe` 來訂閱相關的事件，這裡只訂閱了 `create`

```html
<script>
    Parse.initialize('appid');
    Parse.serverURL = 'https://cashparse.herokuapp.com/parse';
	var query = new Parse.Query('Posts');
	query.subscribe().on('create', function (data) {
        console.log(data);
    });
</script>
```

- 預設支援 `Live Query` 的 classes 的只有 `Posts` 和 `Comments`

![](/images/404.webp)

- 打開網頁就可以看到它和 Parse Server 建立了一條 WebSocket

![](/images/404.webp)

- 使用 curl 測試推資料到 Parse Server，可以看到網頁就會及時收到資料了

> 這段一定要用動態的方式才看的出來 !!

![](/images/404.webp)

- 對照 Dashboard 可以看到有 3 筆資料

![](/images/404.webp)

> 基本上這個 Live Query 功能已經可以取代 SignalR 了 XD
> 其它詳細的 API 用法請參考[官方 SDK](https://docs.parseplatform.org/js/guide/#live-queries)