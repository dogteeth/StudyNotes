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


#### 旋轉view

```Swift


override func viewDidLoad() {
        super.viewDidLoad()

        let rotation = UIRotationGestureRecognizer(
          target: self,
          action: #selector(rotation))

        self.view.addGestureRecognizer(rotation)
        

    }
    

@objc func rotation(recognizer:UIRotationGestureRecognizer) {
        // 弧度
        let radian = recognizer.rotation

        // 旋轉的弧度轉換為角度
        let angle = radian * (180 / CGFloat(Double.pi))

        wheelDrawView.transform =
            CGAffineTransform(rotationAngle: radian)

        print("旋轉角度： \(angle)")
    }




```
