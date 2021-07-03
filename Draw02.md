- [參考1](https://www.raywenderlich.com/10317653-calayer-tutorial-for-ios-getting-started)
- [參考2](https://www.calayer.com/core-animation/2016/05/22/cashapelayer-in-depth.html)



#### 什麼是CAShapeLayer？
- The "CA" in CAShapeLayer stands for CoreAnimation.
- If you wish to animate, move, manipulate, or well, anything else to a UIBezierPath, you need to use a CALayer (or it's subclass CAShapeLayer).
- UIView handles many things, including layout and touch events. However, it doesn’t directly control drawing or animations. UIKit delegates that task to the Core Animation framework, which enables the use of CALayer. UIView, in fact, is just a wrapper over CALayer.
- Each UIView has one root CALayer, which can contain multiple sublayers. When you set bounds on a UIView, the view in turn sets bounds on its backing CALayer. If you call layoutIfNeeded() on a UIView, the call gets forwarded to the root CALayer.
- Layers can have sublayers: Just like views can have subviews, layers can have sublayers. You can use these for some cool effects!
- Their properties are animatable: When you change the property of a layer, you can use CAAnimation to animate the changes.
- Layers are lightweight: Layers are lighter weight than views, and therefore help you achieve better performance.
They have tons of useful properties: You’ll explore some of them in the following examples.


#### layer可以操作的變數
```swift
//1
layer.frame = viewForLayer.bounds
layer.contents = UIImage(named: "star")?.cgImage

// 2
layer.contentsGravity = .center
layer.magnificationFilter = .linear

// 3
layer.cornerRadius = 100.0
layer.borderWidth = 12.0
layer.borderColor = UIColor.white.cgColor
layer.backgroundColor = swiftOrangeColor.cgColor

//4
layer.shadowOpacity = 0.75
layer.shadowOffset = CGSize(width: 0, height: 3)
layer.shadowRadius = 3.0
layer.isGeometryFlipped = false

```

- CALayer has two additional properties that improve performance: shouldRasterize and drawsAsynchronously.
- shouldRasterize is false by default. When set to true, the layer’s contents only render once, which improves performance. It’s perfect for objects that animate around the screen but don’t change in appearance.
- drawsAsynchronously is the opposite of shouldRasterize, and it’s also false by default. Set it to true to improve performance when the app needs to repeatedly redraw a layer’s contents. This might happen, for example, when you work with an emitter layer that continuously renders animated particles. You’ll use this feature later in the tutorial.

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
- 
![example](https://user-images.githubusercontent.com/18608853/122165839-5d997680-ceab-11eb-96bf-ba3ab272d7e3.png)


- UIView handles many things, including layout and touch events. However, it doesn’t directly control drawing or animations. UIKit delegates that task to the Core Animation framework, which enables the use of CALayer. UIView, in fact, is just a wrapper over CALayer.
Each UIView has one root CALayer, which can contain multiple sublayers. When you set bounds on a UIView, the view in turn sets bounds on its backing CALayer. If you call layoutIfNeeded() on a UIView, the call gets forwarded to the root CALayer.

- Layers can have sublayers: Just like views can have subviews, layers can have sublayers. You can use these for some cool effects!
- Their properties are animatable: When you change the property of a layer, you can use CAAnimation to animate the changes.
- Layers are lightweight: Layers are lighter weight than views, and therefore help you achieve better performance.


