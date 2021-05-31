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

案例2

```Swift

import UIKit

class DrawView : UIView {
    override func draw(_ rect: CGRect) {
        
        c2(radiusLength: 100, s_angel: 270, e_angle: 30)

    }
    
    
    func c2(radiusLength:CGFloat, s_angel:CGFloat, e_angle : CGFloat ){
        
        
        let path = UIBezierPath(
            arcCenter: CGPoint(x: 250, y: 250),
            radius: radiusLength,
            startAngle: CGFloat.pi / 180 * s_angel,
            endAngle: CGFloat.pi / 180 * e_angle,
            clockwise: true)
        
        path.lineWidth = 100
        
        path.stroke()
       
        let shapeLayer = CAShapeLayer()

        shapeLayer.path = path.cgPath
        shapeLayer.strokeColor = UIColor(red: 255/255, green: 0/255, blue: 0/255, alpha: 1).cgColor
      
        
        view.layer.addSublayer(shapeLayer)
    
    }
    
}


let view = DrawView(frame: CGRect(x: 0, y: 0, width: 500, height: 500))

view.backgroundColor = .gray


```


#### 三角函數概念
- 知道 1. 圓半徑，2.內角角度，即可取得座標軸。
- sin(θ)
- cos(θ)
- tan(θ)
- 圓周 ＝ 半徑 X 2 X PI
- angle 1 度 ＝ 圓周/360


![001](https://user-images.githubusercontent.com/18608853/120089867-bdb0be80-c130-11eb-8de1-22d7d57e048e.jpg)

#### 三角函數的練習
[youtube](https://www.youtube.com/watch?v=G4D_EhPi7Qk&list=WL&index=227)
[文字](https://yasuoyuhao.medium.com/如何用swift畫圓-利用三角函數畫圓-53d5bd569c0f)
  


#### 取得基本數據

- bounds: The bounds rectangle, which describes the view’s location and size in its own coordinate system.

```Swift
bounds.size.width
bounds.size.height
```
也可以直接用？
```Swift
bounds.width
bounds.height
```

#### ViewController與UIView class之間的練習
- UIView加入 IBOutlet，即可以用IBOutlet的來操作UIView class裹的Method.
notes: 所以 IBOutlet就是class的 init的意思嗎？



#### raywenderlich.com
[連結](https://www.raywenderlich.com/8003281-core-graphics-tutorial-getting-started)


- IBDesignable
- IBInspectable
- Interface Builder = IB


> Any drawing done in draw(_:) goes into the view’s graphics context. Be aware that if you draw outside of draw(_:), you’ll have to create your own graphics context.
