#### Frame 和 Bounds的差別
- Frame => 相對於 Super View 的位置和大小。
- Bounds => 相對於自己的位置和大小，也就是說如果沒有去重設 Bounds 的話，座標永遠都是(0, 0)。

- 加入greenView, 從superView的 x:200, y:200開始，greenView本身的大小為 width 100, height 300
```Swift
greenView.frame = CGRect(x:200, y:200, width:100, height:300)
view.addSubview(grennView)
```

#### 自製 UIView Module
-  以 protocol的方式來進行

```Swift
import UIKit

protocol CustomViewProtocol {
    var contentView: UIView! { get }
    func commonInit(for customViewName: String)
}

extension CustomViewProtocol where Self:UIView {
    
    func commonInit(for customViewName: String) {
        Bundle.main.loadNibNamed(customViewName, owner: self, options: nil)
        
        addSubview(contentView)
        contentView.backgroundColor = .clear
        contentView.frame = bounds
        contentView.autoresizingMask = [.flexibleHeight, .flexibleWidth]
    }

   
    
}
```
- 建立完Protocol後，建立Cocoa Touch Class的 UIView Class

```Swift
import UIKit

class UserGuideMode01: UIView, CustomViewProtocol {
    
    
    @IBOutlet var contentView: UIView!
    
    
    @IBOutlet weak var imageView: UIImageView!
    @IBOutlet weak var subtitleLabel: UILabel!
    @IBOutlet weak var descriptionLabel: UILabel!
    
    required init?(coder: NSCoder) {
        super.init(coder: coder)
        commonInit(for: "UserGuideMode01")
    }
    
    override init(frame: CGRect) {
        super.init(frame: frame)
        commonInit(for: "UserGuideMode01")
    }
    
    //以下是 optional
    func config(inputSubTitle:String, inputDescription:String) {
        
        subtitleLabel.text = inputSubTitle
        descriptionLabel.text = inputDescription
    }
    
    func addBottomBorder(with color: UIColor?, andWidth borderWidth: CGFloat) {
        let border = UIView()
        border.backgroundColor = color
        border.autoresizingMask = [.flexibleWidth, .flexibleTopMargin]
        border.frame = CGRect(x: 0, y: frame.size.height - borderWidth, width: frame.size.width, height: borderWidth)
        addSubview(border)
    }
}
```
- 建立 xib file
在PlaceHolders > File Owner加入 Class的名稱，即可以把兩個Swift File和 Xib File連在一起。 

<img width="1101" alt="01" src="https://user-images.githubusercontent.com/18608853/141239614-24241a30-ae8c-4d75-ae5f-ecdc1d8147ed.png">

#### 讓view的上面左右兩角呈㘣形
[資料來源](https://www.appcoda.com.tw/rounded-corners-uiview/)
```Swift
  func roundCorners(inputView:UIView, cornerRadius: Double) {

        inputView.layer.cornerRadius = CGFloat(cornerRadius)

        inputView.clipsToBounds = true

        inputView.layer.maskedCorners = [.layerMinXMinYCorner, .layerMaxXMinYCorner]

    }
```



#### [Add Shadow to UIView](https://www.hackingwithswift.com/example-code/uikit/how-to-add-a-shadow-to-a-uiview)
- iOS can dynamically generate shadows for any UIView, and these shadows automatically adjust to fit the shape of the item in question – even following the curves of text inside a UILabel.
- Be warned: generating shadows dynamically is expensive, because iOS has to draw the shadow around the exact shape of your view's contents. If you can, set the shadowPath property to a specific value so that iOS doesn't need to calculate transparency dynamically. 


#### UIView加上邊線
```Swift
func addTopBorder(with color: UIColor?, andWidth borderWidth: CGFloat) {
    let border = UIView()
    border.backgroundColor = color
    border.autoresizingMask = [.flexibleWidth, .flexibleBottomMargin]
    border.frame = CGRect(x: 0, y: 0, width: frame.size.width, height: borderWidth)
    addSubview(border)
}

func addBottomBorder(with color: UIColor?, andWidth borderWidth: CGFloat) {
    let border = UIView()
    border.backgroundColor = color
    border.autoresizingMask = [.flexibleWidth, .flexibleTopMargin]
    border.frame = CGRect(x: 0, y: frame.size.height - borderWidth, width: frame.size.width, height: borderWidth)
    addSubview(border)
}

func addLeftBorder(with color: UIColor?, andWidth borderWidth: CGFloat) {
    let border = UIView()
    border.backgroundColor = color
    border.frame = CGRect(x: 0, y: 0, width: borderWidth, height: frame.size.height)
    border.autoresizingMask = [.flexibleHeight, .flexibleRightMargin]
    addSubview(border)
}

func addRightBorder(with color: UIColor?, andWidth borderWidth: CGFloat) {
    let border = UIView()
    border.backgroundColor = color
    border.autoresizingMask = [.flexibleHeight, .flexibleLeftMargin]
    border.frame = CGRect(x: frame.size.width - borderWidth, y: 0, width: borderWidth, height: frame.size.height)
    addSubview(border)
}
```

#### UIView Add Blur Effect

- Add View
```Swift

var darkBlur:UIBlurEffect = UIBlurEffect()
darkBlur = UIBlurEffect(style: UIBlurEffect.Style.systemUltraThinMaterialLight) //extraLight, light, dark

let blurView = UIVisualEffectView(effect: darkBlur)
blurView.frame = self.view.frame //your view that have any objects
blurView.autoresizingMask = [.flexibleWidth, .flexibleHeight]

self.yourWantToAddView.addSubview(blurView)

```

- Remove view
```Swift
 for subview in yourWantToAddView.subviews {
     if subview is UIVisualEffectView {
     subview.removeFromSuperview()
     }
 }
```

#### 加入陰影
```Swift
let yourView = UIView()
yourView.layer.shadowColor = UIColor.black.cgColor
yourView.layer.shadowOpacity = 1
yourView.layer.shadowOffset = .zero
yourView.layer.shadowRadius = 10
```


#### 加入陰影backgroudView
- 設定var
- 在需要出現的地方，view.addSubview
```Swift
  private lazy var dimmedBackgroundView: UIView = {
    let view = UIView()
    view.translatesAutoresizingMaskIntoConstraints = false
    view.backgroundColor = UIColor.black.withAlphaComponent(0.3)
    return view
  }()
```
