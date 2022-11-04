---
title: Class Diagram 類別圖筆記
date: 2020-10-24 18:05:10
tags:
- UML
- Class Diagram
categories:
- 後端
---
## 緣由

每次需要開發較大型的新功能時，往往需要一併重構或是想新架構，而一個人想出來的架構往往會有許多的盲點，因此就會需要畫簡易的類別圖。類別圖不但可以重新審視自己想的架構，更能加速與其他工程師討論的效率。有鑒於本人時常忘記類別圖各種相依關係的圖示，因此以這篇筆記來幫助我快速恢復記憶。

## 什麼是類別圖 class diagram?

類別圖是 [UML](https://zh.wikipedia.org/wiki/%E7%BB%9F%E4%B8%80%E5%BB%BA%E6%A8%A1%E8%AF%AD%E8%A8%80) 的一種，他透過一個系統中的物件、物件的屬性、物件擁有的方法和物件與物件之間的關係來描述其結構。

## 類別圖符號

類別圖的符號分為兩大類

- 描述物件本身
- 描述物件與物件的關係

### 物件 Object

![](https://upload.cc/i1/2020/10/24/X8s7ax.png)

總共分為三大格

1. 物件名字
2. 物件屬性
    - 前面為屬性名字
    - 冒號後面為屬性型別
3. 物件方法
    - 前面為物件名字
    - 括號內為參數和參數型別
    - 冒號後面為回傳值型別

>
>- +代表公開屬性/函式 public attribute / method
>   任何物件都可以存取和使用
> - -代表私有屬性/函式 private attribute / method
>   只有該物件內部才可以存取和使用
> - #代表保護屬性/函式 protected attribute / method
>   只有該物件和該物件繼承的子物件可以存取和使用

### 關係 Relation

- Realization

    ![](https://upload.cc/i1/2020/10/24/4ObGNm.png)

    - A implement B , Ａ 實作 B
    - B 為介面
- Generalization

    ![](https://upload.cc/i1/2020/10/24/v9roc6.png)

    - A extend B, A 繼承 B
    - B 為父類別
- Dependency

    ![](https://upload.cc/i1/2020/10/24/YKRArv.png)

    - A references B, A 使用 B
    - A 在參數或回傳時有用到 B
- Association

    ![](https://upload.cc/i1/2020/10/24/UYHCuv.png)

    - A has-a B object, A 擁有 B
    - B 為 A 擁有的變數

Aggregation 和 Composition 為 Association 的一種特例

![](https://upload.cc/i1/2020/10/24/W7JpMX.png =200x200)

- Aggregation

    ![](https://upload.cc/i1/2020/10/24/pLaJZU.png)

    - A 是由 B 組合而成，且為弱關係
    - A 和 B 擁有自己的獨立的生命週期，B 可單獨存在
    - 舉例
        >訂單 擁有 商品
        >商品可以獨立存在

- Composition

    ![](https://upload.cc/i1/2020/10/24/fmYrAl.png)

    - A 是由 B 組合而成，且為強關係
    - B 只要離開 A 便不具意義，無法單獨存在，且生命週期與 A 一樣
    - 舉例
      >人 擁有 手、腳、頭
      >手、腳、頭獨立存在時無意義

## 參考資料

- [What is class diagram?](https://www.visual-paradigm.com/guide/uml-unified-modeling-language/what-is-class-diagram/)
- [【UML】Class Diagram 類別圖 (下)：Relationships 關係](https://spicyboyd.blogspot.com/2018/07/umlclass-diagram-relationships.html)