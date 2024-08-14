---
title: MAC 安裝 OpenJDK
description: MAC 安裝 OpenJDK
date: 2019-04-16 17:03:46.935+08:00
slug: "mac-ox-install-open-jdk"
tags: [  mac ]
---

- 先到 [首頁](https://jdk.java.net/) 點選要下載的版本，在這裡選的是 JDK11

![](/images/404.webp)

- 來到下載頁面下載 macOS 的版本，目前的版本是 `11.0.2`

![](/images/404.webp)

- 解壓縮

```shell
tar xvf openjdk-11.0.2_osx-x64_bin.tar.gz
```

- 搬到相對應的系統資料夾

```shell
sudo mv jdk-11.0.2.jdk /Library/Java/JavaVirtualMachines
```

- 修改 JAVA_HOME

```shell
export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk-11.0.2.jdk/Contents/Home
```

- 檢查 JAVA 版本

![](/images/404.webp)