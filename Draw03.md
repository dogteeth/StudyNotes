#### 單一做法

```Swift

    func draw01(){
       
        let wid = bounds.width
        let hei = bounds.height
        let center: CGPoint = CGPoint(x: wid/2, y: hei/2)
        let shapLayer = CAShapeLayer()
        shapLayer.lineWidth = lineWidth
        shapLayer.strokeColor = UIColor.green.cgColor

        let linePath = UIBezierPath()
        linePath.move(to: center)
        linePath.addLine(to: CGPoint(x: 50, y: 100))
        
        shapLayer.path = linePath.cgPath
        layer.addSublayer(shapLayer)

    }

```
