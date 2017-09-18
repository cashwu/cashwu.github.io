---
title: EntityFramework Override SaveChange
tags:
  - ef
categories: []
date: 2015-06-11 08:00:00
---

```csharp
public partial class ContosoUniversityEntities  
{
    public override int SaveChanges()
    {
        var entities = this.ChangeTracker.Entries(); // 變更追蹤器，取得所有快取的物件

        foreach (var entity in entities)
        {
            if (entity.Entity is Course)
            {
                if (entity.State == EntityState.Modified)
                {
                    //var ori = entity.OriginalValues.GetValue<string>("Title");
                    //var cur = entity.CurrentValues.GetValue<string>("Title");
                    //取得有修改欄位的原始值和修改後的值

                    entity.CurrentValues.SetValues(new { ModifiedOn = DateTime.Now });
                }
            }
        }

        return base.SaveChanges();
    }
}
```