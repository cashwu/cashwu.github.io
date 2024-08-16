---
title: Ubuntu - 安裝 Java
summary: Ubuntu 安裝 Java
date: 2018-12-20 11:13:38.167+08:00
tags: [ ubuntu ]
draft: false
---

## 檢查 Java 版本

如果直接下 `java --version` 的話，會建議你安裝 `openjdk`，或是 `default` 的 `jre`，如果沒有任何版本的需求的話，就直接安裝 `default` 的就好了

![](/static/images/404.webp)

## 安裝

```shell
sudo apt install default-jre
```

## 驗證

安裝完成之後在下一次 `java --version`，就可以看到安裝了 `OpenJDK` 10.0.2 的版本

![](/static/images/404.webp)

## 設置 JAVA_HOME

- 查尋 java 的安裝路徑

```shell
sudo update-alternatives --config java
```

![](/static/images/404.webp)

- 編輯 `environment`，加入一行設定，路徑就是剛才查尋出來的路徑

```shell
sudo vim /etc/environment
```

```shell
JAVA_HOME="/usr/lib/jvm/java-11-openjdk-amd64/bin/"
```

- Reload environment

```shell
source /etc/environment
```

- 檢查 JAVA_HOME

![](/static/images/404.webp)