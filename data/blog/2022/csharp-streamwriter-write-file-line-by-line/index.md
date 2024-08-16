---
title: C# StreamWriter write file line by line
summary: 因為要寫一個小工具需要逐行寫入檔案，突然想到之前有寫過兩篇文章 C# - Simple StreamWriter and StreamReader 和 C# - Simple FileStream Write and Read，結果好像沒有逐行寫檔的程式碼，簡單的記錄一下使用 StreamWriter 來逐行寫檔
date: 2022-08-13T11:28:04+08:00
tags: [ c# ]
draft: false
---

![](./cover.webp)

因為要寫一個小工具需要逐行寫入檔案，突然想到之前有寫過兩篇文章 [C# - Simple StreamWriter and StreamReader](https://blog.cashwu.com/blog/csharp-simple-filestream-write-and-read) 和 [C# - Simple FileStream Write and Read](https://blog.cashwu.com/blog/csharp-simple-streamwriter-and-streamreader)，結果好像沒有逐行寫檔的程式碼，簡單的記錄一下使用 `StreamWriter` 來逐行寫檔

### 同步

```C#
var list = new List<string>();
using var sw = new StreamWriter(path, true);

foreach (var line in list)
{
    sw.WriteLine(line);
}

sw.Flush();
sw.Close();
```

### 非同步

```C#
var list = new List<string>();
await using var sw = new StreamWriter(path, true);

foreach (var line in list)
{
	await sw.WriteLineAsync(line);
}

await sw.FlushAsync();
sw.Close();
```

> 圖片來源 [Unsplash](https://unsplash.com/photos/AVYo3X6XZYg?utm_source=unsplash&utm_medium=referral&utm_content=creditShareLink)