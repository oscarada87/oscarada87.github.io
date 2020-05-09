---
title: 免費 SSL 憑證申請
tags:
- SSL
- HTTPS
categories:
- SSL
- 隨筆分享
---

# 免費 SSL 憑證申請

[Let’s Encrypt](https://letsencrypt.org/zh-tw/) 是一個可以免費申請 SSL 憑證的機構
最簡單的做法是透過 [Certbot](https://certbot.eff.org/) 來替你的網站安裝憑證
![](https://hackmd.io/_uploads/SJCA2DMcL.png)
![](https://hackmd.io/_uploads/HyqyTPfqU.png)


---

### 以下範例用的是 Ubuntu 16.04 + Nginx
1. 首先要先 SSH 進到你的 server 並擁有 root 權限
2. 下載 Certbot 資源
  ```shell=
  sudo apt-get update
  sudo apt-get install software-properties-common
  sudo add-apt-repository universe
  sudo add-apt-repository ppa:certbot/certbot
  sudo apt-get update
  ```
3. 安裝 Certbot
```shell=
sudo apt-get install certbot python3-certbot-nginx
```
4. 執行
```shell=
sudo certbot --nginx
```
5. 測試更新 bash script
> 因為 Let's Encrypt 發行的憑證 90 天後就會過期，因此每1個半月就需要更新一次，而 Certbot 會幫你安裝一個自動更新的 bash script
> 通常安裝在其中一個這邊的位置
  ```shell=
  /etc/crontab/
  /etc/cron.*/*
  systemctl list-timers
  ```
  檢查更新程式
  ```shell=
  sudo certbot renew --dry-run
  ```
6. 驗證 SSL 安裝成功
可以在 [SSL checker](https://www.sslshopper.com/ssl-checker.html) 檢查有沒有安裝成功
