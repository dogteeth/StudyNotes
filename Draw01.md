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


> Never call draw(_:) directly. If your view is not being updated, then call setNeedsDisplay().
setNeedsDisplay() does not itself call draw(_:), but it flags the view as “dirty,” triggering a redraw using draw(_:) on the next screen update cycle. Even if you call setNeedsDisplay() five times in the same method, you’ll call draw(_:) only once.

##### 畫圖的主要步驟
- setup a path : let plusPath = UIBezierPath()
- set the line width : plusPath.lineWidth = Constants.plusLineWidth
- set the start point : plusPath.move(to: CGPoint)
- set the end point : plusPath.addLine(to: CGPoint)
- set the stroke color : UIColor.white.setStroke()
- begin to draw : plusPath.stroke()

```Swift

override func draw(_ rect: CGRect) {
        let path = UIBezierPath(ovalIn: rect)
        UIColor.blue.setFill()
        path.fill()
        
        let plusWidth = min(bounds.width, bounds.height)
          * Constants.plusButtonScale
        let halfPlusWidth = plusWidth / 2
       
        
        let plusPath = UIBezierPath()
        
        
        plusPath.lineWidth = Constants.plusLineWidth
        plusPath.move(to: CGPoint(
          x: halfWidth - halfPlusWidth,
          y: halfHeight))
        plusPath.addLine(to: CGPoint(
          x: halfWidth + halfPlusWidth,
          y: halfHeight))
        UIColor.white.setStroke()
        plusPath.stroke()

    }

```

- VC controll UIView的關鍵在於 how to  passing value to UIView and forced to re-draw
- passing value to UIView, 利用VC的 IBOute 去取得value ex: countView.countNum += 1
- 在UIView的 value地方，必需加上 setNeedsDisplay()，只要value被修正，它就會呼叫draw，重新畫一次。

在vc的設計

```Swift
class ViewController: UIViewController {

    @IBOutlet weak var countView: CountView!
    
    override func viewDidLoad() {
        super.viewDidLoad()
        // Do any additional setup after loading the view.
    }

    @IBAction func setCountNumBTN(_ sender: MainBTN) {
        
        print("you pressed")
        countView.countNum += 1
    }
}
```
在 UIView的設計

```Swift
import UIKit

class CountView: UIView {
 
    @IBInspectable var countNum : Int = 0 {
        didSet {
            setNeedsDisplay()
        }
    }
    
    @IBInspectable var counterColor: UIColor = UIColor.lightGray
    @IBInspectable var meetColor: UIColor = UIColor.darkGray

    
    override func draw(_ rect: CGRect) {

        print(countNum)
        
        let doubleRadius = max(bounds.width, bounds.height)
        
        let viewWidth = bounds.width
        let viewHieght = bounds.height
        
        let center = CGPoint(x: viewWidth/2, y: viewHieght/2)
        
        
        let path = UIBezierPath(
                    arcCenter: center,
            radius: doubleRadius/2 * 0.6,
                    startAngle: CGFloat.pi / 180 * 270,
            endAngle: CGFloat.pi / 180 * (270+360),
            clockwise: true)
        path.lineWidth = 100
        counterColor.setStroke()
        path.stroke()
        
        
       //meet
        
        
        
        let path2 = UIBezierPath(
                    arcCenter: center,
            radius: doubleRadius/2 * 0.6,
                    startAngle: CGFloat.pi / 180 * 270,
            endAngle: CGFloat.pi / 180 * CGFloat((270 + countNum*10 )),
            clockwise: true)
        path2.lineWidth = 100
        meetColor.setStroke()
        path2.stroke()

        
    }
    

}

```

#### 加入 Animation 的圖表

```Swift
import UIKit

class PieChartView: UIView {
    
    var countNum : Int = 0 {
        didSet {
            setNeedsDisplay()
        }
    }
    
    var counterColor: UIColor = UIColor.lightGray
    var meetColor: UIColor = UIColor.darkGray
    
    override func draw(_ rect: CGRect) {
        
        print(countNum)
                
        
        let doubleRadius = max(bounds.width, bounds.height)
        
        let viewWidth = bounds.width
        let viewHieght = bounds.height
        let radius = doubleRadius/2 * 0.6
        let center = CGPoint(x: viewWidth/2, y: viewHieght/2)
        let lineWidth : CGFloat = 70
        let durationTime : Int = 1
        
        let path = UIBezierPath(
                    arcCenter: center,
            radius: radius,
                    startAngle: CGFloat.pi / 180 * 270,
            endAngle: CGFloat.pi / 180 * (270+360),
            clockwise: true)

        let shapeLayer = CAShapeLayer()
        shapeLayer.fillColor = #colorLiteral(red: 0, green: 0, blue: 0, alpha: 0) .cgColor

        shapeLayer.strokeColor = counterColor.cgColor
        shapeLayer.lineWidth = lineWidth
        shapeLayer.path = path.cgPath
        shapeLayer.strokeStart = 0.0

        layer.addSublayer(shapeLayer)
        
        
        //得到的進度

        let path2 = UIBezierPath(
                    arcCenter: center,
            radius: radius,
                    startAngle: CGFloat.pi / 180 * 270,
            endAngle: CGFloat.pi / 180 * CGFloat((280 +  countNum)),
            clockwise: true)
        path2.lineWidth = lineWidth
        
        
        let shapeLayer2 = CAShapeLayer()
        shapeLayer2.fillColor = #colorLiteral(red: 0, green: 0, blue: 0, alpha: 0) .cgColor

        shapeLayer2.strokeColor = meetColor.cgColor
        shapeLayer2.lineWidth = lineWidth
        shapeLayer2.path = path2.cgPath
        shapeLayer2.strokeStart = 0.0

        let startAnimation2 = CABasicAnimation(keyPath: "strokeStart")
        
        startAnimation2.fromValue = 0
        startAnimation2.toValue = 0.0
        
        let endAnimation2 = CABasicAnimation(keyPath: "strokeEnd")
        endAnimation2.fromValue = 0.2
        endAnimation2.toValue = 1.0
        
        
        let animation2 = CAAnimationGroup()
        animation2.animations = [startAnimation2, endAnimation2]
        animation2.duration = CFTimeInterval(durationTime)
        shapeLayer2.add(animation2, forKey: "MyAnimation")
        
        layer.addSublayer(shapeLayer2)
        
        
    }
    

}


```

#### 視圖區縮小的方式
- .insetBy(dx:CGFloat, dy:CGFloat)
