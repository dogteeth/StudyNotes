- [參考1](https://www.raywenderlich.com/10317653-calayer-tutorial-for-ios-getting-started)
- [參考2](https://www.calayer.com/core-animation/2016/05/22/cashapelayer-in-depth.html)



#### 什麼是CAShapeLayer？
- The "CA" in CAShapeLayer stands for CoreAnimation.
- If you wish to animate, move, manipulate, or well, anything else to a UIBezierPath, you need to use a CALayer (or it's subclass CAShapeLayer).
- UIView handles many things, including layout and touch events. However, it doesn’t directly control drawing or animations. UIKit delegates that task to the Core Animation framework, which enables the use of CALayer. UIView, in fact, is just a wrapper over CALayer.

#### 如何使用CAShapeLayer
- make a instance of CAShapeLayer, let shapeLayer = CAShapeLayer()
- using this instance to setup all the details of the subjects.
- make a instance of UIBezierPath() according to the setup of the shapeLayer.
- 然後，把 UIBezierPath pass 給 CAShapeLayer(!!!!不懂為什麼要這麼麻煩）
- 完成結尾。

```Swift

let shapeLayer = CAShapeLayer()

shapeLayer.bounds = CGRect(x: 0.0, y: 0.0, width: 120.0, height: 120.0)
shapeLayer.lineWidth = 2.0
shapeLayer.fillColor = nil
shapeLayer.path = UIBezierPath(rect: shapeLayer.bounds).cgPath

shapeLayer.strokeColor = UIColor.red.cgColor
layer.addSublayer(shapeLayer)

```

- CGAffineTransfrom
```swift
var pathTransform  = CGAffineTransform.identity
pathTransform = pathTransform.translatedBy(x: center.x, y: center.y)
pathTransform = pathTransform.rotated(by: CGFloat(-.pi / 2.0))
pathTransform = pathTransform.translatedBy(x: -center.x, y: -center.y)
```


#### [2D影像座標轉換](https://iter01.com/420914.html)
- translation
- euclidean
- similarilty
- affine
- projective


#### 仿射變換 affine transformation
- identiy
- translation
- rotation
- isotropic(Uniform Scaling)
- scaling
- reflection
- shear!
![example](https://user-images.githubusercontent.com/18608853/122165839-5d997680-ceab-11eb-96bf-ba3ab272d7e3.png)



