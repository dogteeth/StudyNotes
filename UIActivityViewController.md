####分享的內容
- 圖片，文字，連結
- 不同的平台可接受的內容有差。譬如line無法接受圖片分享


#### A view controller that you use to offer standard services from your app.

- 分享連結的BTN
```Swift
@IBAction func tapToShareCase(_ sender: UIBarButtonItem) {
        print("tap")
        
        guard let safeItem = item else {return }
        
        let sharingCaseName = safeItem.caseName ?? ""
        let sharingCaseInfo = Helper.assembleItemInfo(item: safeItem, assembleOutput: 1)
        
        let sharingText = "\(sharingCaseName) - \(sharingCaseInfo)"
        let itemId : String  = String(safeItem.caseId)
        
        let text = sharingText
        let image = UIImage(named: itemId)
        
        let deepLink = NSURL(string:"https://www.economist.com")
        let shareAll = [text , image! , deepLink! ] as [Any]
        let activityViewController = UIActivityViewController(activityItems: shareAll, applicationActivities: nil)
            activityViewController.popoverPresentationController?.sourceView = self.view
        self.present(activityViewController, animated: true, completion: nil)
    }
```

[參考連結](https://jjeremy-xue.medium.com/swift-玩玩-uiactivityviewcontroller-5995bb80ff68)
三步驟如下：
- 把image, text, link 打包成一個any陣列。
- 使用UIActivityViewController的API
- 做present

```Swift
@IBAction func shareInfo(_ sender: UIButton) {
    // activityItems 陣列中放入我們想要使用的元件，這邊我們放入使用者圖片、使用者名稱及個人部落格。
    // 這邊因為我們確認裡面有值，所以使用驚嘆號強制解包。
    
    let activityVC = UIActivityViewController(activityItems: [userImage.image!,userName.text!,userBlog.text!], applicationActivities: nil)
    // 顯示出我們的 activityVC。
    self.present(activityVC, animated: true, completion: nil)
}
```
