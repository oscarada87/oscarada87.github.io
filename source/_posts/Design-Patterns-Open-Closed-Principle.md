---
title: 'Design Patterns : Open-Closed Principle'
date: 2019-05-24 22:33:21
tags: 
- Design Pattern
- OCP Principle
categories:
- Design Pattern
---
## Open-Closed Principle 開放-封閉法則

#### 核心概念

**:zap:Open for extension, but closed for modification.:zap:**

翻譯成中文↓

**:zap:開放擴充，但避免不必要的修改。:zap:**

![黑人問號](http://i.imgur.com/Es8RWvb.jpg)
還是看不懂嗎?那我來講個故事。

<!-- more -->

假設今天教授要小明寫一個計算學期末總成績的程式，接著小明花了 1 天就用 python 寫出來了，教授覺得你很棒。過了1年後，教授改變了學期總成績的算法，原本的程式就不能用了，這時候你會選擇改程式還是重寫呢?

#### Python範例程式碼
假設每學期都一定會有 4 個成績，期中考、期末考、作業、平時成績。
107 年教授以下表作為學期總成績計算。

| 成績 | 比重 |
| :-: | :-: |
| 期中考 | 25% |
| 期末考 | 35% |
| 作業 | 30% |
| 平時成績 | 10% |

```Python
def finalScore(midterm, finalExam, assignment, usual):
    score = midterm * 0.25 + finalExam * 0.35 + assignment * 0.3 + usual * 0.1
    print('Final Score: {}'.format(score))
    return score
```

小明交了上面的程式之後，教授覺得不好用，每個學生的成績應該是登記好的呀，於是你創建了 Student 這個 class 在寫了一次。

```Python
class Student:
    def __init__(self, name, midterm, finalExam, assignment, usual):
        self.name = name
        self.midterm = midterm
        self.finalExam = finalExam
        self.assignment = assignment
        self.usual = usual
    def finalScore(self):
        score = self.midterm * 0.25 + self.finalExam * 0.35 + self.assignment * 0.3 + self.usual * 0.1
        print('{}\'s final score: {}'.format(self.name, score))
        return score

# Ben 100 100 100 100   學期總成績應為: 100
# Alex 50 75 32 85      學期總成績應為: 56.85
# Peter 46 89 32 90     學期總成績應為: 61.25
# 測試
Ben = Student('Ben', 100, 100, 100, 100)
Alex = Student('Alex', 50, 75, 32, 85)
Peter = Student('Peter', 46, 89, 32, 90)
Ben.finalScore()
Alex.finalScore()
Peter.finalScore()
```

教授很滿意，但還是把你當掉，於是隔了一年再修同一堂課時教授又要求你寫一個學期成績的算法，因為算法不一樣了，改成下表。

| 成績 | 比重 |
| :-: | :-: |
| 期中考 | 30% |
| 期末考 | 30% |
| 作業 | 20% |
| 平時成績 | 20% |
| 加分 | 數字多少加幾分 |

這時候如果有套用 OCP 原則就可以很輕鬆地改了。

```Python
import abc

class Student(abc.ABC):
    def __init__(self, name, midterm, finalExam, assignment, usual):
        self.name = name
        self.midterm = midterm
        self.finalExam = finalExam
        self.assignment = assignment
        self.usual = usual
    # 建立抽象function- finalScore
    @abc.abstractmethod
    def finalScore(self):
        return NotImplemented

# 去年學生
class Student107(Student):
    def __init__(self, name, midterm, finalExam, assignment, usual):
        # 呼叫父類別的init函式
        super(Student107, self).__init__(name, midterm, finalExam, assignment, usual)
    # 實作finalScore
    def finalScore(self):
        score = self.midterm * 0.25 + self.finalExam * 0.35 + self.assignment * 0.3 + self.usual * 0.1
        print('{}\'s final score: {}'.format(self.name, score))
        return score
        
# 測試     
# Ben 100 100 100 100    學期總成績應為: 100
# XioMing 50 75 32 85    學期總成績應為: 56.85
# Peter 46 89 32 90      學期總成績應為: 61.25

Ben = Student107('Ben', 100, 100, 100, 100)
XioMing = Student107('XioMing', 50, 75, 32, 85)
Peter = Student107('Peter', 46, 89, 32, 90)
print('107 Students:')
Ben.finalScore()
XioMing.finalScore()
Peter.finalScore()

# 今年學生
class Student108(Student):
    def __init__(self, name, midterm, finalExam, assignment, usual, addPoint):
        # 呼叫父類別的init函式
        super(Student108, self).__init__(name, midterm, finalExam, assignment, usual)
        # 新增 加分 這個新的屬性
        self.addPoint = addPoint
    # 實作finalScore
    def finalScore(self):
        score = self.midterm * 0.3 + self.finalExam * 0.3 + self.assignment * 0.2 + self.usual * 0.2 + self.addPoint
        print('{}\'s final score: {}'.format(self.name, score))
        return score
        
# 測試
# Brian 100 100 100 100 3 學期總成績應為: 103
# XioMing 50 75 32 85 5   學期總成績應為: 65.9
# Apple 46 89 32 90 0     學期總成績應為: 64.9

Brian = Student108('Brian', 100, 100, 100, 100, 3)
XioMing = Student108('XioMing', 50, 75, 32, 85, 5)
Apple = Student108('Apple', 46, 89, 32, 90, 0)
print('108 Students:')
Brian.finalScore()
XioMing.finalScore()
Apple.finalScore()

```

以後每年成績算法不同只要新增一個class繼承Student再覆寫學期總成績算法就行了，小明也靠著加分過了那堂課!

:tada:可喜可賀:tada:可喜可賀:tada:

#### 參考資料
1. [談談OCP - 輕鬆談軟工 - 台灣軟體工程學會](http://blog.seat.org.tw/2009/03/ocp.html)
2. [搞笑談軟工: 亂談軟體設計（2）：Open-Closed Principle](http://teddy-chen-tw.blogspot.com/2011/12/2.html)