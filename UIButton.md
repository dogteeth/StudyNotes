#### UIButton 更改文字
```Swift
button.setTitle("Button Title", for: .normal)

```

#### UIButton 更改圖片
```Swift
itemsNearByButton.setImage(UIImage(systemName: "chevron.up"), for: .normal)
```


#### [EdgeInset](http://shinancao.cn/2016/12/15/iOS-UIButton-EdgeInsets/)
- 如果没有给UIButton的宽和高一个固定值，那么UIButon的大小将自动调整为正好放下title和image。
- UIEdgeInset的設定，並不會改變button的大小，只會改變內容位置的定位。


#### contentEdgeInsets, 設UIEdgeInsets後的觀察
- button的intrinsic的長寛，是依內容物決定，剛好把內容物放完。
- 設了contentEdgeInsets後，內容物外會再多一圈padding. padding會把button撐大。
- 但如果button有用autolayout constraints宣告大小，如：spotifyButton.heightAnchor.constraint(equalToConstant: buttonHeight)，則button的大小就會依contraints的進行。


#### UIButton的基本設定
- button.titleLabel?.minimumScaleFactor = 0.5 // default 0, Button內之文字顯示，最低的字級大小
- button.titleLabel?.adjustsFontSizeToFitWidth = true // default false, 是否允許Button內的字体自動調整級數做顯示。
- 



```Swift
button.contentEdgeInsets = UIEdgeInsets(top: 30, left: buttonHeight, bottom: 30, right: buttonHeight)
```

##### [來源](https://stackoverflow.com/questions/51150926/custom-uibutton-class-with-animation-swift)


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
#### 自製BTN
```Swift
import UIKit

@IBDesignable
final class CoyoteButton: UIButton {

    var borderWidth: CGFloat = 2.0
    var borderColor = UIColor.white.cgColor

    @IBInspectable var titleText: String? {
        didSet {
            self.setTitle(titleText, for: .normal)
            self.setTitleColor(UIColor.black,for: .normal)
        }
    }

    override init(frame: CGRect){
        super.init(frame: frame)
    }

    required init?(coder: NSCoder) {
        fatalError("init(coder:) has not been implemented")
    }

    override func layoutSubviews() {
        super.layoutSubviews()
        setup()
    }

    func setup() {
        self.clipsToBounds = true
        self.layer.cornerRadius = self.frame.size.width / 2.0
        self.layer.borderColor = borderColor
        self.layer.borderWidth = borderWidth
    }
}
```
