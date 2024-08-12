---
title: Heroku - PostgreSQL Backup
description: 前面的文章已經用 ASP.NET Core MVC 接了 Heroku 的 PostgreSQL，現在要來看怎麼備份 PostgreSQL
date: 2018-12-14 13:30:08.063+08:00
slug: "heroku-postgresql-backup"
tags: [  heroku , postgresql ]
---

前面的文章已經用 ASP.NET Core MVC 接了 Heroku 的 PostgreSQL ([ASP.NET Core MVC - 使用 Heroku 的 PostgreSQL](https://blog.cashwu.com/blog/asp-net-core-mvc-heroku-postgresql))，現在要來看怎麼備份 PostgreSQL

## 手動備份 - 使用 CLI

- 進到專案目錄，下 `heroku pg:backups:capture` 作 backup，完成後會給你一個 id，以下面來看就是 `b001`
- 如果在備份的途中想要停止，可以下 `heroku pg:backups:cancel`


![](/images/404.webp)

- 如果想要查看相關的資訊，可以下 `heroku pg:backups:info`

![](/images/404.webp)

- 你也可以把備份檔下載到本地 `heroku pg:backups:download b001` ( b001 是備份成功時的 id )

![](/images/404.webp)

## 手動備份 - 使用畫面

- 先來到 Database 的畫面，點 `Durability` Tab

![](/images/404.webp)

- 畫面下方就可以看到 `MANUAL BACKUPS & DATA EXPORTS` 區塊，點 `Create Manual Backup` 手動備份，下方就可以看到它的狀態，備份完成之後就可以下載或是刪除了

![](/images/404.webp)

## 周期性備份

- 目前要設定週期性備份的話只能使用 CLI，`heroku pg:backups:schedule --at '00:00 Asia/Taipei'`，後面的時區可以參考 [List of tz database time zones](https://en.wikipedia.org/wiki/List_of_tz_database_time_zones)

![](/images/404.webp)

- 使用 `heroku pg:backups:schedules` 查詢

![](/images/404.webp)

- 如果要取消可以使用 `heroku pg:backups:unschedule`

![](/images/404.webp)

## 狀態

- 可以使用 `heroku pg:backups` 查看目前的備份狀態

![](/images/404.webp)

##限制

- 不同計畫的手動備份是有限制的，請看官方的[說明](https://devcenter.heroku.com/articles/heroku-postgres-backups#manual-backup-retention-limits)
- 周期性備份的存放時間可以看官方的[說明](https://devcenter.heroku.com/articles/heroku-postgres-backups#scheduled-backups-retention-limits)