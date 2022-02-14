#### 甚麼是 viewDidLoad？
Apple 對於 viewDidLoad 的定義，是它會在 Controller 的視圖被載入記憶體後 被呼叫。簡單來說，即是第一個載入的方法。你可能會想：到底在甚麼情況下會充分利用這個方法？答案是：依你希望 App 首先載入的東西而定，例如：你想把背景顏色從白色更換成藍色。

#### 甚麼是 viewDidAppear?
Apple 將其定義為「通知 View Controller 視圖已經被加進視圖階層裡。」換句話說，就是當畫面呈現在使用者眼前時，就呼叫這個方法。viewDidAppear 與 viewDidLoad 的不同之處，在於每次進入畫面時 viewDidAppear 就會被呼叫，而 viewDidLoad 只會在 App 加載時被呼叫一次。

#### 甚麼是 viewDidLayoutSubviews?
- Apple 針對 viewDidLayoutSubviews 給了一個很好的解釋：呼叫 viewDidLayoutSubviews，就可以通知 View Controller 它的視圖剛放置好子視圖內。換句話說，每次當視圖更新、旋轉、更動或是 bounds change 時就會呼叫 viewDidLayoutSubviews。這段解釋的關鍵字就是 bounds change。

- 但是要知道，viewDidLayoutSubviews 只會在視圖上所有 Auto Layout 設定或是大小自動計算完成後才會執行，這表示當每次視圖的大小改變或是佈局重新計算時就會呼叫 viewDidLayoutSubviews 方法。

- 每當你 Build App 時，viewDidLayoutSubviews 就會在 viewDidLoad 之後執行，因為 viewDidLayoutSubviews 是在佈局計算後被呼叫。然後當你旋轉 App 時，viewDidLayoutSubviews 就會再次執行，不過這次只會在橫式與直式互換時執行，而從左換到右時則不會執行。


#### view.layoutIfNeeded()
- Lays out the subviews immediately, if layout updates are pending.
#### view.setNeedsLayout()
- Invalidates the current layout of the receiver and triggers a layout update during the next update cycle.


#### View Dismiss
[source](https://stackoverflow.com/questions/28760541/programmatically-go-back-to-previous-viewcontroller-in-swift)

```Swift
    //to previous view
    navigationController?.popViewController(animated: true)
    //to root view
    navigationController?.popToRootViewController(animated: true)
```
