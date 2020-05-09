---
title: 用 Python 打造自己的 Telegram Bot!
date: 2019-05-25 11:53:10
tags:
- Python
- Telegram Bot
categories:
- Python
---
## Telegram Bot 教學
這邊我們使用 Python 3.6↑ 與 telepot進行示範
[telepot 文件](http://telepot.readthedocs.io/en/latest/)


#### 安裝 telepot 和 pprint 套件
```
pip install telepot
pip install telepot --upgrade  # 更新
pip install pprint # 讓 print 出來的文字自動排版
```
<!--more-->

#### 取得 telegram bot Token
跟 BotFather 對話輸入 /newbot
![](https://i.imgur.com/HjRUO0m.png)

接著要輸入 **名字** (bot的顯示名稱) 和 **username** (bot的使用者ID)

:warning:注意 username 必須是 bot 結尾

![](https://i.imgur.com/qvZzpcH.png)
接著 BotFather 會給你一組 Token (紅色遮掉的地方)

#### 測試是否有連上自己的 bot

```Python
import telepot
bot = telepot.Bot('***** PUT YOUR TOKEN HERE *****')
print(bot.getMe())
```
![](https://i.imgur.com/kuRWgHq.png)

執行結果應該能看到自己 bot 的 id, is_bot, name, username :tada:


#### 從 telegram 上接收訊息

```Python
import telepot
import time
from telepot.loop import MessageLoop
from pprint import pprint

bot = telepot.Bot('***** PUT YOUR TOKEN HERE *****')

def handle(msg):
    pprint(msg)

MessageLoop(bot, handle).run_as_thread()
print("I'm listening...")

while 1:
    time.sleep(5)

```
![](https://i.imgur.com/EKwBxSp.png)

一般發送出來的訊息會長這個 Json 格式 :tada:


![](https://i.imgur.com/4uBaUSh.png)

Inline Query 的訊息會長這個 Json 格式 :tada:

> Inline Query 是指在 telegram 中以 @標記bot 輸入的文字而不送出
> ![](https://i.imgur.com/Xp1wwCh.png)

##### 我比較常用到的屬性

| 屬性 | 描述 |
| :----- | :----------- |
| chat_id | 每個房間都有一個聊天室 id，不管是私聊還是大群，這個屬性幾乎是必抓，因為這樣才能讓 bot 知道要回在哪個群組中。 |
| from_username   | 用戶的 username，可以用在標記 user 上 |
| from_id | 用戶的 id，可以用在 inline 標記上 |
| message_id | 用戶訊息的 id，可以用在 reply 上 |
| id | 用戶 inline query 的 id，可以用在 reply 上 |
| text | 用戶的訊息內容 |
| query | 用戶的 inline query 內容 |

#### 用 bot 回訊息在 telegram 上

```Python
bot.sendMessage(chat_id, text, parse_mode=None, disable_web_page_preview=None, disable_notification=None, reply_to_message_id=None, reply_markup=None)
```
[官方API文件](https://core.telegram.org/bots/api#sendmessage)


```Python
import telepot
import time
from telepot.loop import MessageLoop
from pprint import pprint

bot = telepot.Bot('***** PUT YOUR TOKEN HERE *****')

def handle(msg):
    pprint(msg)
    chat_id = msg['chat']['id']
    from_id = msg['from']['id']
    text = msg['text']
    
    bot.sendMessage(chat_id, text)

MessageLoop(bot, handle).run_as_thread()
print("I'm listening...")

while 1:
    time.sleep(5)
```
上面這段程式碼會讓 bot 當個鸚鵡，重複任何你打的字!

#### 用 bot 回圖片在 telegram 上

```Python
bot.sendPhoto(chat_id, photo, caption=None, parse_mode=None, disable_notification=None, reply_to_message_id=None, reply_markup=None)
```
[官方API文件](https://core.telegram.org/bots/api#sendphoto)


```Python
import telepot
import time
from telepot.loop import MessageLoop
from pprint import pprint

bot = telepot.Bot('***** PUT YOUR TOKEN HERE *****')

def handle(msg):
    pprint(msg)
    chat_id = msg['chat']['id']
    from_id = msg['from']['id']
    photo = 'https://pic.pimg.tw/like9417/1504869777-564645577.jpg?v=1504869878'
    
    bot.sendPhoto(chat_id, photo)

MessageLoop(bot, handle).run_as_thread()
print("I'm listening...")

while 1:
    time.sleep(5)
```
上面這段程式碼會讓 bot 傳梗圖，你打任何字都會回你梗圖!