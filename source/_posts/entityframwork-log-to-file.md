---
title: EntityFramwork Log to File
tags:
  - ef
categories: []
date: 2015-06-12 08:00:00
---

將 EF 產生的 T-SQL 語法記錄到檔案

```csahrp
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