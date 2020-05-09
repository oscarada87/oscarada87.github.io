---
title: 第三方API封裝 Third Party API Encapsulation
date: 2019-11-22 01:29:55
tags:
- Design Pattern
- Refactor
categories:
- Design Pattern
- Refactor
---

# Refactor 之路

此系列文章是為了記錄 Refactor 公司遺留程式碼，一方面以後可以回過頭來檢討，一方面可以讓更多人一起討論。
主要會寫一些 design choice 以及架構設計的 UML 圖。

### 第三方API封裝 Third Party API Encapsulation
![Service Diagram](https://user-images.githubusercontent.com/20165488/69312439-e6b5e080-0c69-11ea-9a6a-23f82aac7c3c.png)

Service 主要負責三件事
- input validation (輸入驗證)
validation 寫在 service 的好處是，如果未來 validation 有更動，就不需要到各個 adapter 修改
- output format (輸出格式)
統一不同介面的 API 回傳格式
介面可按需求自行調整，主要是為了讓每支 API 有共通的操作介面
- HTTP request encapsulation (封裝)
封裝後可以隱藏實作細節，並重複使用

