---
title: EntityFramework DbEntityEntry State
tags:
  - ef
categories: []
date: 2015-06-11 08:00:00
---


```csharp
using (var db = new ContosoUniversityEntities())  
{
    var c = db.Course.Find(1);

    var ce = db.Entry(c);
    Console.WriteLine(ce.State); // unchanged

    c.Title += ".";

    //Console.WriteLine(ce.State); // unchanged
    // Entry 是取得當下物件的快照，所以如果物件有任何異動的話，需要在取一次
    Console.WriteLine(db.Entry(c).State); // Modified

    db.Course.Remove(c);
    Console.WriteLine(db.Entry(c).State); // Deleted

    db.Entry(c).State = System.Data.Entity.EntityState.Unchanged;
    db.SaveChanges(); // SaveChanges會沒有作用，因為目前的狀態是 unchanged 
}
```