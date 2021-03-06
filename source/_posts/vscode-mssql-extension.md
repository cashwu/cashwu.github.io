---
title: VSCode - mssql Extension
tags:
  - vscode
categories: []
date: 2017-01-02 10:19:33
---

微軟出了一個 Visual Studio Code 的擴充套件 [mssql](https://marketplace.visualstudio.com/items?itemName=ms-mssql.mssql) 可以不用使用 SSMS 就可以簡易的操作 MS SQL，不過這個套件現在還在 Preview 階段，希望未來會有愈來愈多的功能

這是 MS 出的如何使用這個套的教學 [Use the mssql extension for Visual Studio Code](https://docs.microsoft.com/en-us/sql/linux/sql-server-linux-develop-use-vscode)

這是國外的一篇 Blog 說 DBA 如何使用 Visual Studio Code 來管理 [Introduction of Visual Studio Code for DBAs](https://www.sqlshack.com/introduction-visual-studio-code-dbas/)

下面簡單的記錄一下如何使用這個套件

## Install Extension

- 搜尋 mssql 並且安裝

![](./vscode-mssql-extension/01.png)

- 新增一個檔案，並按右下角 `Plain Text`

![](./vscode-mssql-extension/02.png)

- 選擇 `SQL`

![](./vscode-mssql-extension/03.png)

- 第一次會先下載相關的檔案然後安裝

![](./vscode-mssql-extension/04.png)

## Connect DB

- 安裝完後 `Show All Commands` ( `Ctrl+Shift+P` )，搜尋 `sql`，選擇 `Connect` 連結到 DB

![](./vscode-mssql-extension/05.png)

- 第一次的話都沒有任何的 Connection Profile 所以要先 Create 一個

![](./vscode-mssql-extension/06.png)

- 輸入 Server name

![](./vscode-mssql-extension/07.png)

- 在這裡輸入的是本機的 sql express

![](./vscode-mssql-extension/08.png)

- 輸入要連接的 DB 名稱，不輸入的話為預設值 ( `master DB` )

![](./vscode-mssql-extension/09.png)

- 選擇認證的方式

![](./vscode-mssql-extension/10.png)

- 最後給 profile 一個名字

![](./vscode-mssql-extension/11.png)

- 如果輸入的資料都沒有問題，而且可以正常的連接到 DB 的話，右下角會顯示連結的資訊，點連結資訊的話會出現 DB 讓你選

![](./vscode-mssql-extension/12.png)

- 在這裡選擇北風資料庫

![](./vscode-mssql-extension/13.png)

- 右下角的資訊就會出現目前連接到北風資料庫

![](./vscode-mssql-extension/14.png)

- 當下一次再選擇連結資料庫的時候就會出現剛才新增的 `local` Profile

![](./vscode-mssql-extension/15.png)

## Query DB

- 在檔案格式是 `SQL` 的情況下打 sql 就會有 intellisense 出現

![](./vscode-mssql-extension/16.png)

- 選擇 `sqlSelect` 的話就會出現基本的語法

![](./vscode-mssql-extension/17.png)

- 打 DB name、Table Name 和 Column 的話也會有 intellisense

![](./vscode-mssql-extension/18.png)

![](./vscode-mssql-extension/19.png)

![](./vscode-mssql-extension/20.png)

- 打完 SQL Command 之後在空白處按右鍵會有 `Execute Query` 的選項

![](./vscode-mssql-extension/21.png)

- 選擇 `Execute Query` 的話就會出現另外一個 `Results` 視窗，呈現 Query 後的結果

![](./vscode-mssql-extension/22.png)

- 而在 Results 視窗的最右邊有兩個選項 `Save as JSON` 和 `Save as CSV`，你可以把結果給存下來

![](./vscode-mssql-extension/23.png)

![](./vscode-mssql-extension/24.png)

- 選擇 `Save as JSON` 的話會叫你輸入存檔的位置，這裡記得要輸入附檔名

![](./vscode-mssql-extension/25.png)

![](./vscode-mssql-extension/26.png)

- 輸出後會出現 `Info` 提示你已經存檔成功，並且會開另外一個視窗呈現輸出的檔案內容

![](./vscode-mssql-extension/27.png)

- 下面是 CSV 的內容

![](./vscode-mssql-extension/28.png)

## Change Results Layout

- 在 SSMS 裡面，結果的話一般預設都是在 Command 的下面，如果覺得 Visual Studio Code 預設是左右的話，可以在選項裡面選擇 `Toggle Editor Group Layout`

![](./vscode-mssql-extension/29.png)

- Results 視窗就會出現在下面

![](./vscode-mssql-extension/30.png)