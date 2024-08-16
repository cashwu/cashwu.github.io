---
title: C# - compare string is null or empty
summary: C# - compare string is null or empty
date: 2016-01-18 19:49:14.279+08:00
tags: [ c# ]
draft: false
---

There have 3 string variable

```csharp
string strA = null; // null  
string strB = ""; // empty  
string strC = " "; // whitespace  
```

1.using `==` , just can found out is null or is empty single

```csharp
(strA == null) //true
(strB == null) //false
(strC == null) //false
(strA == "") //false
(strB == "") //true
(strC == "") //false
```
2.using `trim()` extension can found out is empty or is whitespace, but maybe have throw exception when the string is null

```csharp
(strA.Trim() == "") //throw exception
(strB.Trim() == "") //true
(strC.Trim() == "") //true
```
3.using `string.IsNullOrEmpty` , can found out is null and empty both, but can't found out whitespace

```csharp
string.IsNullOrEmpty(strA) //true  
string.IsNullOrEmpty(strB) //true  
string.IsNullOrEmpty(strC) //false  
```
4.using `string.IsNullOrWhiteSpace` , can found out is null and empty and whitespace, but the method maybe have performance issues

```csharp
string.IsNullOrWhiteSpace(strA) //true  
string.IsNullOrWhiteSpace(strB) //true  
string.IsNullOrWhiteSpace(strC) //true  
```
so, best way is using `string.IsNullOrEmpty()`

if not need have whitespace condition or using `string.IsNullOrWhiteSpace()` have whitespace condition