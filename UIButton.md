[來源](https://stackoverflow.com/questions/51150926/custom-uibutton-class-with-animation-swift)


- Below code when you tap on button it will call animate method and perform animation. 
When you want to perform animation on button just assign AnimatedButton class as Custom Class of UIButton :
```Swift
class AnimatedButton: UIButton {

    override func draw(_ rect: CGRect) {

        self.addTarget(self, action: #selector(animate), for: .touchUpInside)
    }

    @objc func animate() {

        self.transform = CGAffineTransform(scaleX: 0.6, y: 0.6)

    }
}
```

- IBAction加入動畫程式，展示完後再進行action.
```Swift
@IBAction func moutainButtonPressed(_ sender: UIButton) {
        
        
        sender.transform = CGAffineTransform(scaleX: 0.6, y: 0.6)
        
        UIView.animate(withDuration: 1,
                       delay: 0.1,
                       usingSpringWithDamping: CGFloat(0.20),
                       initialSpringVelocity: CGFloat(6.0),
                       options: UIView.AnimationOptions.allowUserInteraction,
                       animations: {
                        sender.transform = CGAffineTransform.identity
                       },
                       completion: { Void in (
                        self.performSegue(withIdentifier: SegueIdentifier.WalkProToTopicsTVC, sender: self)
                        
                       
                       )}
        )
    }
```

- 做extension再做指派
```Swift
class CustomButton:UIButton {
    
    override init(frame: CGRect) {
        super.init(frame: frame)
        configeBtn()
    }
    
    required init?(coder aDecoder: NSCoder) {
        super.init(coder: aDecoder)
        configeBtn()
    }
    
    func configeBtn() {
        
        self.addTarget(self, action: #selector(btnClicked(_:)), for: .touchUpInside)
        
    }
    
    @objc func btnClicked (_ sender:UIButton) {
        
        let animation = CAKeyframeAnimation()
        animation.keyPath = "position.x"
        animation.values = [0,10,-10,10,0]
        animation.keyTimes = [0, 0.16, 0.5, 0.83, 1]
        animation.duration = 0.4
        animation.isAdditive = true
        
        sender.layer.add(animation, forKey: "shake")
        
    }
}
```
