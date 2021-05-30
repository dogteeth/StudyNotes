#### Draw的學習
[連結](https://medium.com/彼得潘的-swift-ios-app-開發教室/ios13-app-swift5-實例說明-使用-uibezierpath來繪製圖案-cc192b3addc5)

notes: 
- UIColor的用法： UIColor(red: 128/255, green: 100/255, blue: 0, alpha: 1) 

##### 簡單的線
- 設定 draw view的背景
- 拉繪圖路徑: let path = UIBezierPath() 
- 設定起始點： path.move(to: CGPoint(x: 100, y: 256))
- 設定中間的點： path.addLine(to:CGPoint(x: 400, y: 256))
- 設定圖層layer: let shapeLayer = CAShapeLayer()
- 將繪圖路徑加到圖層裹： shapeLayer.path = path.cgPath
- 設定繪圖圖層的顏色： shapeLayer.strokeColor = UIColor(red: 255/255, green: 255/255, blue: 255/255, alpha: 1).cgColor
- 將繪圖圖層加到view裹： backgroundView.layer.addSublayer(shapeLayer)

Playground的例子：
```Swift

import UIKit

let backgroundView = UIView(frame: CGRect(x: 0, y: 0, width: 1000, height: 1000))

backgroundView.backgroundColor = UIColor(red: 25/255, green: 24/255, blue: 250/255, alpha: 1)

let path = UIBezierPath()

path.move(to: CGPoint(x: 100, y: 256))
path.addLine(to:CGPoint(x: 400, y: 256))
let shapeLayer = CAShapeLayer()
shapeLayer.path = path.cgPath
shapeLayer.strokeColor = UIColor(red: 255/255, green: 255/255, blue: 255/255, alpha: 1).cgColor
backgroundView.layer.addSublayer(shapeLayer)

backgroundView


```


- sin(θ)
- cos(θ)
- tan(θ)

![001](https://user-images.githubusercontent.com/18608853/120089867-bdb0be80-c130-11eb-8de1-22d7d57e048e.jpg)


  
