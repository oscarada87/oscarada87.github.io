---
title: Side Project 隨筆紀錄 2021-10-16
date: 2021-10-17 00:13:42
tags:
- python
- docker
- postgresql
categories:
- 後端
---

想趁著做 Side Project 的同時順便練習一下文筆，因此就有了這系列的文章，主要是紀錄踩過的坑。 
Side Project 想要使用 flask + postgresql，因此打算要在 windows 10 上安裝 docker，並透過 docker-compose 建立 postgresql 資料庫，而以下就是今天踩到的坑。

## 在 docker-compose 中利用 environment variable

```bash
${VARIABLE_NAME}
```

## psql: FATAL: password authentication failed for user "postgres"

```bash
# docker-compose.yml
version: '3.8'

services:
  db:
    image: postgres
    restart: always
    environment:
      - POSTGRES_USER=${POSTGRES_USER}
      - POSTGRES_PASSWORD=${POSTGRES_PASSWORD}
      - POSTGRES_DB=${POSTGRES_DB}
    ports:
      - "5432:5432"
    volumes:
      - postgres-data:/var/lib/postgresql/data

volumes:

  postgres-data:
```

在 docker container 裡建立的 postgresql 沒辦法連進去，兩個方法可以試試看

1. 刪掉 docker volume 後重新跑一次
    
    有可能是因為在建立 container 時一樣用到舊 volume 資料，導致 docker-compose 或 docker file 上的設定沒有套用。
    
2. 將對外的 port 從改成 5432 改成別的 `5433:5432`
    
    > 前面的數字代表 container 向外對應到 windows 上的 port，後面的數字則是 container 內的 port
    > 
    
    因為 5432 是 postgresql 預設的 port，所以假如在 windows 本機上也有裝 postgresql 的話，不管是透過 pgAdmin 或下 `psql` 指令連線都會連到 windows 本機上的 postgresql，而不是 docker container 裡的。
    

## pipenv shell 中沒有辦法使用箭頭上跟下來輸入之前的指令

在 power shell 而不是 cmd 中執行 pipenv shell 就可以解決。