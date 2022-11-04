---
title: Hexo 常用指令
date: 2021-10-16 19:45:47
tags:
- hexo
- node js
categories:
- 其他
---

把一些常用的 hexo 指令記錄下來，以免每次都要重新查

- 建立新文章
    
    ```bash
    hexo new [layout] <title>
    ```
    
- 產生 static file
    
    ```bash
    hexo generate
    ```
    
    在 deploy 到 github 之前需要先打這行指令
    可以在後面接上 `-d` 或 `--deploy` 就可以直接發布
    
    > `hexo generate -d` 跟 `hexo deploy -g` 是一樣的
    > 
- 在 local 開 server
    
    ```bash
    hexo deploy -p 5000
    ```
    
    `-p` 指令 port
    
- 列出所有路徑
    
    ```bash
    hexo list <type>
    ```
    
    type 打 `post` 可以拿到所有發布的文章
    
- 清理快取和產生的檔案
    
    ```bash
    hexo clean
    ```