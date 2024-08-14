---
title: EntityFramework - Log to File
description: EntityFramework Log to File
date: 2015-06-12 22:26:03.937+08:00
slug: "entityframework-log-to-file"
tags: [ ef ]
---

將 EF 產生的 T-SQL 語法記錄到檔案

```csharp
using (var db = new ContosoUniversityEntities())  
{
    db.Database.Log = (log) =>
    {
        System.IO.File.AppendAllText(@"Z:\log.txt", "\r\n");
        System.IO.File.AppendAllText(@"Z:\log.txt", log);
    };

    var c = db.Course.Find(1);
    var name = c.Department.Name;
}
```

### 注意事項

> 目前可以使用的版本為 EF6