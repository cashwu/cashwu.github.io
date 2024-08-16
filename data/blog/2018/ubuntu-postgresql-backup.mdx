---
title: Ubuntu - PostgreSQL Backup
summary: 備份在 Ubuntu 上面的 PostgreSQL
date: 2018-12-14 16:30:19.761+08:00
tags: [ postgresql , ubuntu ]
draft: false
---

請面的文章已經安裝好 PostgreSQL 了 ([Ubuntu - 安裝 PostgreSQL](https://blog.cashwu.com/blog/ubuntu-install-postgresql))，現在要來看怎麼備份 PostgreSQL

## 備份

- 把需要備份的 Database 相關的帳號和密碼存在使用者的 `Home` 資料夾下面，檔名為 `.pgpass`，格式如下
	- hostname:port:database:username:password

```shell
127.0.0.1:5432:testdb:cash:cash
```

- 備份主要用的 command 是 `pg_dump`，基本的參數如下
	- h - ip
	- p - port
	- U - user
	- d - database

- 可以使用 gzip 壓縮

```shell
pg_dump -h 127.0.0.1 -p 5432 -U cash -d testdb | gzip > /home/cash/testdb.pgsql.gz
pg_dump -h 127.0.0.1 -p 5432 -U cash -d testdb > /home/cash/testdb.dump
pg_dump -h 127.0.0.1 -p 5432 -U cash -d testdb > /home/cash/testdb.bak
```

## 還原

- 還原的話要看當初備份出來的檔案是什麼，用的命令不太一樣， `.bak` 的話要用  `pg_restore`，`.dump` 和 `.pgsql` 的話要用 `psql`
	- 如果是 `gz` 的話要用 `gunzip` 先解壓縮
	- 還原的話，資料庫需要存在，如果不存在的話會出現錯誤

```shell
gunzip testdb.pgsql.gz
psql -h 127.0.0.1 -p 5432 -U cash -d testdb < testdb.pgsql

psql -h 127.0.0.1 -p 5432 -U cash -d testdb < testdb.dump

pg_restore -h 127.0.0.1 -p 5432 -U cash -d testdb < testdb.bak
```

## 定期備份

- 可以寫個 `shell` 檔，然後定期去執行它，下面為 `shell` 檔的內容
	- 時間變數設定為每天

```shell
#!/usr/bin/env bash

#設定時間變數
day=$(date +%Y%m%d)
#設定備份路徑
bkdir="/home/cash"
#備份資料庫
pg_dump -h 127.0.0.1 -p 5432 -U cash -d testdb | gzip > "$bkdir"/testdb."$day".pgsql.gz

exit 0
```