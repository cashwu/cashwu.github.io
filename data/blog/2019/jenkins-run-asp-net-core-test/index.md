---
title: Jenkins 執行 ASP.NET Core 測試
description: Jenkins 如何執行 ASP.NET Core 測試然後顯示測試結果
date: 2019-04-25 10:38:45.58+08:00
slug: "jenkins-run-asp-net-core-test"
tags:  [ asp.net core , jenkins ]
---

之前的文章 ( [Jenkins 建置 ASP.NET Core 專案](https://blog.cashwu.com/blog/jenkins-build-asp-net-core) ) 已經可以建置專案了，現在就來看如何執行測試，然後顯示測試結果

## 測試程式

- 在 solution 裡面有測試專案 `TestJenkins.Test`，裡面有一個簡單的測試

```csharp
public class HomeControllerTests
{
    [Fact]
    public void Index()
    {
        var controller = new HomeController();
        var actionResult = controller.Index();

        var viewResult = actionResult as ViewResult;
        Assert.NotNull(viewResult);
    }
}
```

## 加入執行測試

- 來到專案的`設定頁面`，在原本的建置步驟下面在多一個步驟 `執行 Shell`

![](/images/404.webp)

- 參考官方的指令 [dotnet test](https://docs.microsoft.com/zh-tw/dotnet/core/tools/dotnet-test?tabs=netcore21)，使用 `dotnet test` + 專案檔就可以執行測試

```shell
dotnet test ./TestJenkins.Test/TestJenkins.Test.csproj
```

![](/images/404.webp)

## 測試執行測試

- 手動建置專案，可以看到有跑測試了，而且是成功的

![](/images/404.webp)

## 產生測試報告

- 可以使用 `--logger` 產生執行的記錄，把原本的 shell 修改成

```shell
dotnet test ./TestJenkins.Test/TestJenkins.Test.csproj --logger "trx;LogFileName=unit_tests.xml"
```

- 再一次建置專案，可以看到有產生測試報告出來

![](/images/404.webp)

## Jenkins 顯示測試結果

- 來到 Jenkins 的 `設定` 頁面，選擇 `管理外掛程式`

![](/images/404.webp)

- 點選 `可用的` 頁籤，在右上角的 `過濾條件` 打 `xunit`，然後選擇 `xUnit`，點選 `直接安裝`

![](/images/404.webp)

- 等到變成 `藍燈 成功`，就好了

![](/images/404.webp)

- 回到專案的設定頁面，到最下面的 `建置後動作` 區塊

![](/images/404.webp)

- 選擇 `Publish xUnit test result report`

![](/images/404.webp)

![](/images/404.webp)

- `Report Type` 的地方選擇 `MSTest-Version`

> 注意：不要選成 `xUnit` 了

![](/images/404.webp)

- 填入產出 report 的路徑，如果不確定路徑的話，可以看一下執行的內容，就是 `workspace` 後面的路徑，因自己已經是 `TestJenkins`，所以路徑從下一層開始

![](/images/404.webp)

![](/images/404.webp)

- 儲存之後重新建置一次，就可以看到頁面上多了一個 `最近測試結果`

![](/images/404.webp)

- 點進去就可以看到相關的記錄

![](/images/404.webp)

- 如果執行兩次以上右邊就會出現圖表

![](/images/404.webp)