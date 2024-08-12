---
title: C# - CLI、CIL、CLR 和 CTS
description: C# CLI、CIL、CLR 和 CTS
date: 2015-01-06 08:27:48.197+08:00
slug: "csharp-cli-cil-clr-cts"
tags: [ c# ]
---

## Common Language Infrastructure (CLI) 
### 通用語言基礎架構

- 開放的技術規範，定義了構成 `.net Framework` 基礎結構的可執行碼以及代碼的執行時環境的規範
- 它定義了一個語言無關的跨體系結構的執行環境，這使得開發者可以用規範內定義的各種高階語言來開發軟體，並且無需修正即可將軟體執行在不同的電腦體系結構上 (跨平台)
- CLI 規範的程式都是編譯成 `通用中間語言 (CIL)` ，之後在執行過程中被虛擬執行系統的 `即時編譯技術(JIT)` 編譯為 `機器碼(Native Code)` 執行


## Common Intermediate Language (CIL) 
### 通用中間語言

- `微軟中間語言 Microsoft Intermediate Language (MSIL)`
- `低階（lowest-level）` 的人類可讀的程式語言 


## Common Language Runtime (CLR)
### 通用語言執行平台

- 是 .net 的虛擬機器，它是微軟對 CLI 的實作版本

![](/images/404.webp)

![](/images/404.webp)

> 以上圖片來自 MSDN

## Common Type System (CTS)
### 通用型別系統

- 定義型別在 `執行時期(Runtime)` 如何宣告、使用及管理
- 在執行時期提供 `跨語言整合(Cross-Language Integration)` 的功能
- 所有的型別都是由 `基底型別(Base Type) System.Object` 所衍生
- C# 的型別以別名 (Alias) 的方式來對應 .net framework 中的型別
- [.NET Framework 所提供基底型別的清單、簡要說明各型別](http://msdn.microsoft.com/zh-tw/library/hfa3fa08.aspx)