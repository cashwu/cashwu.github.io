---
title: EntityFramework Disabled LazyLoading Load Data
tags:
  - ef
categories: []
date: 2015-06-12 08:00:00
---


關閉 LazyLoading 後，手動載入資料的作法

```csharp
using (var db = new ContosoUniversityEntities())  
{
    db.Configuration.LazyLoadingEnabled = false;

    var c = db.Course.Find(1);

    // 載入單筆資料時 (導覽屬性)
    db.Entry(c).Reference(a => a.Department).Load();

    // 載入多筆資料時 (導覽屬性集合)
    db.Entry(c).Collection(a => a.Person).Load();
}
```