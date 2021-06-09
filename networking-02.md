[Reusable Image Cache in Swift](https://medium.com/flawless-app-stories/reusable-image-cache-in-swift-9b90eb338e8d)


- Using NSCache as a storage
- Memory FootPrint
  - pages of memory
  - typically 16 kb in size
  - numbers of pages  X page size = Memory in Use
  - 50 kb的 image, = 3 pages and less than 1 page.
 
An app has three kinds of memory
- clean: 
- dirty: app 寫進去的所有資料都算 dirty
- compressed: compressed the pages not in use, and decompressed when in use.


當 App 進入背景或重新啟動時，圖片將需要重新抓取。因為當 App 進入背景時，NSCache 裡的內容會被移除。 而當 App 重新啟動時， NSCache 也會重新產生，不會有之前儲存的資料。


做法
- 生成 NSCache instance
- 在 loadImage的地方，NSCache有圖時，即用NSCache。
- 在 loadImage的地方，NSCache沒有圖時，Load圖的同時，並進行Cache。

```swift

let imageCache = NSCache<NSURL, UIImage>()

func loadImage(_ urlString:String) {
        
        guard let nsurlString = NSURL(string: urlString.urlEncoded()) else {return}
        if let imageFromCache = imageCache.object(forKey: nsurlString as NSURL) {
            imageView.image = imageFromCache
            return
        }
        
        let spin = imageView.activityIndicator
        spin.startAnimating()
        
        if let url = URL(string: urlString.urlEncoded()) {
            
            let task  = URLSession.shared.dataTask(with: url) { data, respons, error in
                guard let data = data, error == nil else {return}
                
                guard let newImage = UIImage(data:data) else {return}
                self.imageCache.setObject(newImage, forKey: nsurlString )
                
                DispatchQueue.main.async {
                    self.imageView.image = UIImage(data: data)
                    spin.stopAnimating()
                }
            }
            task.resume()
        }
        
    }
```
