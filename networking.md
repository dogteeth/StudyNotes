##### Grand Central Dispatch
[GCD](https://learnappmaking.com/grand-central-dispatch-swift/)
[GCD應用](https://franksios.medium.com/ios-gcd%E5%A4%9A%E5%9F%B7%E8%A1%8C%E7%B7%92%E7%9A%84%E8%AA%AA%E6%98%8E%E8%88%87%E6%87%89%E7%94%A8-c69a68d01da1)

- DispatchQueue.main.async{code}: code是在main thread下進行。譬如UI更新。
- DispatchQueue.global().async{code}: code不是在main thread下進行。譬如download data。
- Queues: 是資料結構中的一種型態，翻成中文叫「佇列」。它的特性是先進先出(FIFO, First-in First-out)。
- Serial queues: 這個佇列裡的工作是按照順序執行的，一次只執行一個，當前一個執行完後，才會執行下一個。serial queues 適合拿來處理共享的資源，因為這樣可以確保存取是按照順序來的。
- Concurrent queues: 相對於 serial 就是同時發生的。也是說多個工作是同時被執行的。concurrent queues 代表這個 queues 裡的工作會按順序「開始」執行，但因為是 concurrent ，所以不必等上一個工作執行完才接著執行下一個，因此每個工作執行結果的時間是不可預測的。
- Synchronous: synchronous 的 function 只有在完成裡面的工作後，才會回傳值。
- Asynchronous: 相對於 synchronous，asynchronous 的 function 會馬上回傳值。asynchronous function 裡的工作會按照順序執行，但這個 function 不會等其它的動作執行完，它會馬上回傳值，因此 asynchronous function 不會造成它所在的執行緒阻塞。
- 綜合 Serial、Concurrent 的 Queues，加上 Synchronous 和 Asynchronous 的行為，會 有四種排列組合。
  - concurrentQueue.sync, concurrentQueue.async
  - serialQueue.sync, serialQueue.async
- Dispatch Group的應用：dispatch groups 提供更方便的等待機制，當我們必須等待一個或一個以上的 thread 處理完工作後，再去執行某件事時，就可使用此機制來達成，不過 dispatch groups 有兩種狀況，一是 queue 裡的工作項目都是很單純的個別子執行緒；二是 queue 裡的工作項目除了都是個別的子執行緒外，每個子執行緒裡又有子執行緒，這種狀況實際上非常常見，例如在子執行緒裡又去呼叫後端的 API(後端 API 屬另一條子執行緒)，此時就要用比較特殊的作法來處理。
- 透過 DispatchQueue.main 來取得主執行緒的使用權，block 即可撰寫我們想要做的事，在實務上通常被用來更新 UI，因更新 UI 只能放在主執行緒。
- DispatchQueue.global 產生的 Queues 是 Concurrent 的。

[SwiftPal](https://www.swiftpal.io/articles/how-to-use-gcd-grand-central-dispatch-tutorial)
- Dispatch Queue works in two main ways, which are synchronous execution & asynchronous execution.Synchronous is used when you want to execute only one task at a time. Whereas, Asynchronous means that multiple tasks can be executed at a time regardless of the finishing time, which means if a task needs some time to perform, the other tasks will not have to wait for it to complete.


##### async的提醒：stackoverflow
You are using return instead of using a callback. You are doing your parsing when the network connection is done; asynchronously.
To synchronize it, you'd need to use semaphores, but that is highly discouraged on the main thread.Instead, do the appropriate things with the result when your completion block is executed. Think of the data task as 'do stuff, come back to me when you're done'.
* 在networking的時候，發現可以順利取到值，但是後續加工的程式，郤出現空值。應該是parsing的時間完成和後續加工程式執行上，有時間差，如果是這個問題，設計completion handler，加工程式放在這，待networking處理完後，再接著執行。（待確認：這樣的理解是否正確？）

##### 直接進入google搜尋
```swift
let urlString = "https://www.google.co.in/search?q=" + text 
```
##### 直接連接Wiki頁面搜尋
```Swift
let url = "https://zh.wikipedia.org/wiki/" + text
```

##### threads
- fetching data from API happens on the background thread

##### 什麼是threads
- program：是一群程式的集合
- process：是由program產生的執行個体，多個，process。
- 每一個process各由2個東西組成，1）memory space： (相關於obejct裹的var), 2）thread：作業系統能夠進行運算排程的最小單位。
- thread 代表從某一個起始點開始（例如：main），到目前，所有函數的呼叫路徑，以及這些呼叫路徑上所有到的區域變數cpu內部的暫存器也會一起紀錄。
- thread組成內容：1）stack,紀錄函數，呼叫路徑，及其用到的區域變數。 2）目前cpu的狀態。



#### 打開WEB

##### 三個打開web的方法
- Mobile Safari：以行動版的safari打開指定URL。使用者暫時離開了app，切換到safari
- UIWebView/WKWebView：將網頁嵌進APP裹。WKWebView是UIWebView的改良版。它俱備Nitro JS的引擎。
- SFSafariViewController：最新的工具。讓Safari的功能整合進IOS


##### 取得連結後打開safari
如果該連結有reader模式，以reader模式啟動
```swift
import SafariServices

 if let urlString = URL(string: "http://www.google.com") {

            let config = SFSafariViewController.Configuration()
            config.entersReaderIfAvailable = true
            let vc = SFSafariViewController(url: urlString, configuration: config)
            present(vc, animated: true)
        }

```

#### 另一種寫法
```swift
import SafariServices

if let urlString = URL(string: urlString) {
            UIApplication.shared.open(urlString, options: [:], completionHandler: nil)

```



#### 中文URL的處理
- url的連結中有全形中文或全形空格，需先進行轉碼。
- 轉碼運用到的method需要用到String的extesion。
- .addingPercentEncoding(withAllowedCharacters: .urlQueryAllowed)
- 例子如下：

```swift

class ViewController: UIViewController {
    
   let s3 = "https://data.boch.gov.tw/old_upload/_upload/Assets_new/building/1554/photo/B005 台北市 長老教會北投教堂 (直轄定)01.JPG"
    

    func loadImage(urlString:String) {
        
        if let url = URL(string: urlString.urlEncoded()) {
            let task  = URLSession.shared.dataTask(with: url) { data, respond, error in
                guard let data = data, error == nil else {return}
                
                DispatchQueue.main.async {
                    self.imageView.image = UIImage(data: data)
                }
            }
            
            task.resume()
        }
        
    }
    
}

extension String {
    func urlEncoded() -> String {
           let encodeUrlString = self.addingPercentEncoding(withAllowedCharacters:
               .urlQueryAllowed)
           return encodeUrlString ?? ""
       }
}

```

##### Spin Annimation, while image is loading

- 先做UIImage的extension, 把UIActivityIndicatorView的instance相關需要，在這裹設計。
- 在loadImage相關的function, 宣告一個instance. 用這個instance去做start, stop.


```swift

func loadImage(_ urlString:String) {
        let spin = imageView.activityIndicator
        spin.startAnimating()
        if let url = URL(string: urlString.urlEncoded()) {
            let task  = URLSession.shared.dataTask(with: url) { data, respons, error in
                guard let data = data, error == nil else {return}
                
                DispatchQueue.main.async {
                    self.imageView.image = UIImage(data: data)
                    spin.stopAnimating()
                }
            }
            task.resume()
        }
    }


extension UIImageView {
    fileprivate var activityIndicator : UIActivityIndicatorView {
        get {
            
            let activityIndicator = UIActivityIndicatorView(style: .large)
            activityIndicator.hidesWhenStopped = true
            activityIndicator.center = CGPoint(x:self.frame.width/2, y:self.frame.height/2)
            
            activityIndicator.stopAnimating()
            self.addSubview(activityIndicator)
            return activityIndicator
        }
    }
}
```

#### Loading Image cache的運用

[study](https://medium.com/flawless-app-stories/reusable-image-cache-in-swift-9b90eb338e8d)

[Cache an image with Swift](https://programmingwithswift.com/cache-image-with-swift/)
