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

#### 判斷tap在view裹的所在位置。

```Swift
    override func viewDidLoad() {
        super.viewDidLoad()
        
        let tap = UITapGestureRecognizer(target: self, action: #selector(touchedScreen(touch:)))
        view.addGestureRecognizer(tap)
    }

    
    @objc func touchedScreen(touch: UITapGestureRecognizer) {
        
        //取得tap的所在位置。
        let touchPoint = touch.location(in: pieChartView)
        print(touchPoint)

        let hei = pieChartView.bounds.height
        let wid = pieChartView.bounds.width
        let center = CGPoint(x: wid/2, y: hei/2)

        let dT = center.distance(to: touchPoint)

        print("dt: \(dT)")
        if dT > 100 {
            print("not the circle")
        } else {
            print("in the circle")
        }
        
    }

}

//利用三角含數取得兩點之間的距離。
extension CGPoint {
    func distance(to point: CGPoint) -> CGFloat {
        return sqrt(pow((point.x - x), 2) + pow((point.y - y), 2))
    }
}


```

#### Add LongGestureRecongnizer
```Swift
 private func setupLongGestureRecognizerOnCollection() {
        let longPressedGesture = UILongPressGestureRecognizer(target: self, action: #selector(handleLongPress(gestureRecognizer:)))
        longPressedGesture.minimumPressDuration = 0.5
        longPressedGesture.delegate = self
        longPressedGesture.delaysTouchesBegan = true
        collectionView?.addGestureRecognizer(longPressedGesture)
    }

    @objc func handleLongPress(gestureRecognizer: UILongPressGestureRecognizer) {
        if (gestureRecognizer.state != .began) {
            return
        }

        let p = gestureRecognizer.location(in: collectionView)

        if let indexPath = collectionView?.indexPathForItem(at: p) {
            Helper.centerItemLocation(mapView: mapView, item: casesNearByUserLocation[indexPath.row])
        }
    }
```
