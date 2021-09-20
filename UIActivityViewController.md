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
