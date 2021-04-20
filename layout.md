### Layout

#### 1.
- Constraint-base layout system. 以限制為設計方式的layout.
- Adaptive user interface. 能夠自体適應user的界面規格。
- 以點（point)的方式來進行。points vs pixels

#### 2.
- Align：對齊
- Pin：建立間距約束
- Stack：嵌入堆疊視圖
- Issue：解決約束問題（auto layout issues)

#### 3.
在特定約束的檢閱器裹，可進一步設定，該約束的相關屬性
- 關聯性 relation
- 常數 constant
- 優先權 priority


#### 4.
[Cheating Sheet](https://www.hackingwithswift.com/articles/140/the-auto-layout-cheat-sheet)
auto layout programmatically.

#### 5.
[Basic Tutorial](https://www.raywenderlich.com/1343912-adaptive-layout-tutorial-in-ios-12-getting-started)

#### 6.
[The why, what, and how of Swift Auto-Layout](https://uxdesign.cc/the-why-what-and-how-of-swift-auto-layout-9530a60eedf4)

leading and trailing, 也可是 left and right. 但leading 和 trailing可以依照不同文化習慣改變，譬如由右到左的書寫，leading就是從右開始。


**Attributes Categories**
* Horizontal: left, right, leading, trailing, center-x
* Vertical: top, bottom, center-y
* Size: height and width

**Anatomy of a constraint**
* Participants: the one or two participants attributes.
* Inequalities: the type of relationships between participants.
* Modification: some sort of optionally applied defined changes.



#### 不懂

1. Interface Builder Document
有兩個選項：
Use Auto Layout，
Use Size Classese 《- 這個會變成 自由型式的畫面 freeform canvas.



##### Tips

**Layout Refresh**

Editor > Resolve Auto Layout Issues > Update Frames(有兩個，依狀況選擇）

