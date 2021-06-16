#### 什麼是CAShapeLayer？
- The "CA" in CAShapeLayer stands for CoreAnimation.
- If you wish to animate, move, manipulate, or well, anything else to a UIBezierPath, you need to use a CALayer (or it's subclass CAShapeLayer).
- UIView handles many things, including layout and touch events. However, it doesn’t directly control drawing or animations. UIKit delegates that task to the Core Animation framework, which enables the use of CALayer. UIView, in fact, is just a wrapper over CALayer.
- 
