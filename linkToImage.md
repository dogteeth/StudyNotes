#### 中文URL的處理
- url的連結中有全形中文或全形空格，需先進行轉碼。
- 轉碼運用到的method需要用到String的extesion。
- .addingPercentEncoding(withAllowedCharacters: .urlQueryAllowed)
- 例子如下：

```swift
import UIKit

class ViewController: UIViewController {

    @IBOutlet weak var imageView: UIImageView!
    
    let s1 = "https://data.boch.gov.tw/old_upload/_upload/Assets_new/building/1617/photo/B010 台北市 北投文物館 (直轄定)01.JPG"
    let s2 = "https://data.boch.gov.tw/upload/representImageFile/2021-04-01/13bdb094-e508-467a-8142-00bb424e815a/P_20210319_144805.jpg"
    
    let s3 = "https://data.boch.gov.tw/old_upload/_upload/Assets_new/building/1554/photo/B005 台北市 長老教會北投教堂 (直轄定)01.JPG"
    
    override func viewDidLoad() {
        super.viewDidLoad()
        
        loadImage(urlString: s3)

    }

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


Spin Annimation, while image is loading
[來源](https://stackoverflow.com/questions/58263815/does-xcode-have-a-built-in-loading-animation-for-uiimageview)

```swift

private var activityIndicator: UIActivityIndicatorView {
    let activityIndicator = UIActivityIndicatorView()
    activityIndicator.hidesWhenStopped = true
    self.addSubview(activityIndicator)
}

func setImageFrom(_ urlString: String, completion: (() -> Void? = nil) ) {
    guard let url = URL(string: urlString) else { return }
    
    let session = URLSession(configuration: .default)
    let activityIndicator = self.activityIndicator
    
    DispatchQueue.main.async {
        activityIndicator.startAnimating()
    }
    
    let downloadImageTask = session.dataTask(with: url) { (data, response, error) in
        if let error = error {
            print(error.localizedDescription)
        } else {
            if let imageData = data {
                DispatchQueue.main.async { [weak self] in 
                    var image = UIImage(data: imageData)
                    self?.image = nil
                    self?.image = image
                    image = nil
                    completion?()
                }
            }
        }
        DispatchQueue.main.async {
            activityIndicator.stopAnimating()
            activityIndicator.removeFromSuperview()
        }
        session.finishTasksAndInvalidate()
     }
     downloadImageTask.resume()
} 

```
