##### async的提醒：stackoverflow
You are using return instead of using a callback. You are doing your parsing when the network connection is done; asynchronously.
To synchronize it, you'd need to use semaphores, but that is highly discouraged on the main thread.Instead, do the appropriate things with the result when your completion block is executed. Think of the data task as 'do stuff, come back to me when you're done'.
* 在networking的時候，發現可以順利取到值，但是後續加工的程式，郤出現空值。應該是parsing的時間完成和後續加工程式執行上，有時間差，如果是這個問題，設計completion handler，加工程式放在這，待networking處理完後，再接著執行。（待確認：這樣的理解是否正確？）

##### 直接進入google搜尋
```swift
let urlString = "https://www.google.co.in/search?q=" + text 
```

##### threads
- fetching data from API happens on the background thread

##### 什麼是threads
- program：是一群程式的集合
- process：是由program產生的執行個体，多個，process。
- 每一個process各由2個東西組成，1）memory space： (相關於obejct裹的var), 2）thread：作業系統能夠進行運算排程的最小單位。
- thread 代表從某一個起始點開始（例如：main），到目前，所有函數的呼叫路徑，以及這些呼叫路徑上所有到的區域變數cpu內部的暫存器也會一起紀錄。
- thread組成內容：1）stack,紀錄函數，呼叫路徑，及其用到的區域變數。 2）目前cpu的狀態。
