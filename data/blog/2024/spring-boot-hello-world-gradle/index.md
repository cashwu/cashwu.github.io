---
title: Spring Boot Hello World 從 0 到 1 建立專案 - gradle
description: 不使用範本的方式建立 spring 的專案，而是自己從空的專案建立起來
slug: "spring-boot-hello-world-gradle"
date: 2024-02-17
tags: [ java , springboot ]
---

> 相關的步驟和程式碼，參考自[官方文件]( https://docs.spring.io/spring-boot/docs/current/reference/htmlsingle/#getting-started.first-application)

上一篇文章 [SpringBoot Hello World 從 0 到 1 建立專案 - maven](https://blog.cashwu.com/blog/spring-boot-hello-world-maven/) 是使用 `maven` 建立專案，這篇就來就使用 `gradle` 建立，基本上程式碼的部份都是一樣，只有設定檔不一樣


1. 一樣建立空的專案

2. 在建立 `module` 的時候，選擇 `Gradle`，DSL 選擇 `Groovy`

![](./01.png)

3. 預設的設定檔為 `build.gradle`，裡面會有一些預設的設定

```groovy
plugins {
    id 'java'
}

group = 'com.cashwu'
version = '1.0-SNAPSHOT'

repositories {
    mavenCentral()
}

dependencies {
    testImplementation platform('org.junit:junit-bom:5.9.1')
    testImplementation 'org.junit.jupiter:junit-jupiter'
}

test {
    useJUnitPlatform()
}
```


4. 在 `plugins` 的地方，加入一條 `id`，`dependencies` 的地方，加入一條 `implementation`。另外，要加入一個 `apply plugin`。
 
 基本上，一個就是在 maven 加入的 `parent`，一個就是 `starter`，只是寫法不太一樣，從 `xml` 變成攤平的文字，中間用 `:` 隔開

```groovy
plugins {
    id 'org.springframework.boot' version '3.1.2'
}

apply plugin: 'io.spring.dependency-management'

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
}
```

改完後，把不必要的先移除，設定變成下面這樣，就大功告成了

```groovy
plugins {
    id 'java'
    id 'org.springframework.boot' version '3.2.2'
}

apply plugin: 'io.spring.dependency-management'

group = 'com.cashwu'
version = '0.0.1-SNAPSHOT'

repositories {
    mavenCentral()
}

dependencies {
    implementation 'org.springframework.boot:spring-boot-starter-web'
}
```