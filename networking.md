##### async的提醒：stackoverflow
You are using return instead of using a callback. You are doing your parsing when the network connection is done; asynchronously.
To synchronize it, you'd need to use semaphores, but that is highly discouraged on the main thread.Instead, do the appropriate things with the result when your completion block is executed. Think of the data task as 'do stuff, come back to me when you're done'.
* 在networking的時候，發現可以順利取到值，但是後續加工的程式，郤出現空值。應該是parsing的時間完成和後續加工程式執行上，有時間差，如果是這個問題，設計completion handler，加工程式放在這，待networking處理完後，再接著執行。（待確認：這樣的理解是否正確？）

##### 直接進入google搜尋
```swift
let urlString = "https://www.google.co.in/search?q=" + text 
```

