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
