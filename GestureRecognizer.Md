#### 加入手勢偵測

```Swift
 func gestureRecognizerSetup(){
        let panSwipeToRight = UISwipeGestureRecognizer(target: self, action: #selector(swipeToRight))
        panSwipeToRight.direction = .right
        
        let panSwipeToLeft = UISwipeGestureRecognizer(target: self, action: #selector(swipeToLeft))
        panSwipeToLeft.direction = .left
        
        view.addGestureRecognizer(panSwipeToRight)
        view.addGestureRecognizer(panSwipeToLeft)
    }

    
    @objc func swipeToRight(_ recognizer: UISwipeGestureRecognizer) {

        guard var safeIndex = index else {return}
        if safeIndex > 0 {
            safeIndex =  safeIndex - 1
        }
        index = safeIndex
        item = items?[safeIndex]
        
        tableView.reloadData()
        guard let urlString = item?.representImage else { return }
        loadImage(urlString)
        mapAddAnnotation()
    }
    
    @objc func swipeToLeft(_ recognizer: UIScreenEdgePanGestureRecognizer) {
        if recognizer.state == .recognized {
            
            guard var safeIndex = index else {return}
            guard let totalIndex = items?.count else {return}
            if safeIndex <= totalIndex - 1 {
                safeIndex =  safeIndex + 1
            }
            
            index = safeIndex
            item = items?[safeIndex]
            
            tableView.reloadData()
            guard let urlString = item?.representImage else { return }
            loadImage(urlString)
            mapAddAnnotation()
        }
    }

```
