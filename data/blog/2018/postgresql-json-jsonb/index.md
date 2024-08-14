---
title: PostgreSQL - Json & Jsonb
description: 比較 PostgreSQL 裡面 Json 和 Jsonb 的不同
date: 2018-12-20 13:18:48.974+08:00
slug: "postgresql-json-jsonb"
tags: [ postgresql ]
---

下面會比較 PostgreSQL 裡面 Json 和 Jsonb 的不同

- Jsonb 的 b 是 binary 的意思，也就是說會以 binary 的型式存到 DB 裡面，而 Json 就是以一般文字的型式存在 DB

## 比較差異

- 執行下面沒有 format 過 JSON

```sql
select '{ "name" : "cash" }'::Json
select '{ "name" : "cash" }'::Jsonb
```

- 得到下面的結果，Jsonb 會 format Json 的格式，Json 不會

![](/images/404.webp)

- 執行下面重復 Key 的 Json

```sql
select '{ "name" : "cash", "name" : "gg" }'::Json
select '{ "name" : "cash", "name" : "gg" }'::Jsonb
```

- 得到下面的結果，Jsonb 會移除掉重復 Key 的 Json，會只保留最後一個

![](/images/404.webp)

## 結論

- 存到 DB 的時候，Jsonb 因為需要轉換格式，所以會比 Json 來的慢
- 在 DB 端處理 Json 的話，Jsonb 因為是在 binary 處理，所以 Jsonb 的效能會比 Json 來的好