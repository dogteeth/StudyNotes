#### translatesAutoresizingMaskIntoConstraints
- 預設值為true，系統會auto resize，依狀況判斷。
- 要進行手動設定layout constraints時，要將此值改為false，要系統不要auto resize，全部依照code的定義進行。

#### [iPhone UIKit Size](https://developer.apple.com/library/archive/documentation/DeviceInformation/Reference/iOSDeviceCompatibility/Displays/Displays.html)
- SE:320*568
- 6/7/8/X:375*667
- 7/8Plus:414*736
- iPad/iPadPro 9.7: 768*1024
- iPadPro 10.5: 834*1112
- iPadPro 12.9: 1024*1366



#### 建立Constraint的三種
- storyboard
- NSLayoutAnchor
- NSLayoutConstraint


#### How it works
- leading, trailing, top, bottom
- 4 elements mus have: x, y, height, width
- setup  constraint
```Swift

//Positioning Anchors
label.topAnchor.constraint(
  equalTo: view.topAnchor, //為準的parent view
  constant: 20 // 離parent的距離
  ).isActive = true


//Sizing Anchors
lable.heightAnchor.constraint( //設定height的數字
  equalToContant: 50
  ).isActive = true
  
//Alignment Anchors
lable.centerYAnchor.constraint( //對齊y的中央
  equalTo: view.centerYAnchor //為準的parent view
  ).isActive = true
  
//Baseline Anchors
button1.firstBaselineAnchor.constraint(     //將button1的底線對齊至
  equalTo: multiLabel.firstBaselineAnchor   //至multiLabel的第一行的底線。相對於 lastBaselineAnchor(最後一行的底線）
  ).isActive = true

```

- translatesAutoresizingMaskIntoConstraints : Note that the autoresizing mask constraints fully specify the view’s size and position; therefore, you cannot add additional constraints to modify this size or position without introducing conflicts. If you want to use Auto Layout to dynamically calculate the size and position of your view, you must set this property to false
```Swift
   yourlabel.translatesAutoresizingMaskIntoConstraints = false
```

- 將safe area加入autoLayout的設定
```Swift
  view.safeAreaLayoutGuide.topAnchor
  view.topAnchor
```

#### UILayoutGuides
- SafeAreas：以下的地方都不會被掉。
  - Status bars : 最上面的瀏海
  - Navigation bars
  - Tab bars
  - Tool bars：最下面暗示home screen的一條線
- LayoutMargins
  - 上去掉40， 下去掉34 左右各去掉20（預設值）
- ReadableContent
  - A dynamicllay calculated area that tries to preserve content for reading based on orientation and font size.


#### safeAreaGuide, layoutMarginsGuide
- safeAreaGuide, 上下空白
- layoutMarginGuide, 下左右都空白


```Swift
        NSLayoutConstraint.activate([
            redView.topAnchor.constraint(equalTo: view.layoutMarginsGuide.topAnchor),
            redView.leadingAnchor.constraint(equalTo: view.layoutMarginsGuide.leadingAnchor),
            redView.trailingAnchor.constraint(equalTo: view.layoutMarginsGuide.trailingAnchor),
            redView.bottomAnchor.constraint(equalTo: view.layoutMarginsGuide.bottomAnchor)
        ])
```
#### UILayoutGuide()
- A rectangular area that can interact with Auto Layout.
- Use layout guides to replace the dummy views you may have created to represent inter-view spaces or encapsulation in your user interface. 
- A dummy view is an empty view that does not have any visual elements of its own and serves only to define a rectangular region in the view hierarchy.
- For example, if you wanted to use constraints to define the size or location of an empty space between views, you needed to use a dummy view to represent that space. 
- If you wanted to center a group of objects, you needed a dummy view to contain those objects. Similarly, dummy views could be used to contain and encapsulate part of your user interface.
- Dummy views let you break up a large, complex user interface into self-contained, modular chunks. When used properly, they could greatly simplify your Auto Layout constraint logic.



#### AutoLayout的改變有兩種
- External Change
  - The user resizes the window (OS X).
  - The user enters or leaves Split View on an iPad (iOS).
  - The device rotates (iOS).
  - The active call and audio recording bars appear or disappear (iOS).
  - You want to support different size classes.
  - You want to support different screen sizes.
- Internal Change
  - The content displayed by the app changes.
  - The app supports internationalization.
  - The app supports Dynamic Type (iOS).


#### Tha anatomy of a constraint
![view_formula_2x](https://user-images.githubusercontent.com/18608853/128792076-fbd2cf60-0e61-4d47-8eaa-dcc3c92057ff.png)

- Equality, Not Assignment
- It’s important to note that the equations shown in Note represent equality, not assignment.
- When Auto Layout solves these equations, it does not just assign the value of the right side to the left. Instead, it calculates the value for both attribute 1 and attribute 2 that makes the relationship true.


#### intrinsic content size
- What is a view’s intrinsic content size?
- Most views have an intrinsic content size, which refers to the amount of space the view needs for its content to appear in an ideal state. For example, the intrinsic content size of a UILabel will be the size of the text it contains using whatever font you have configured it to use.
- Intrinsic content sizes are important because they allow views to have a natural width and height without us forcing one. For Auto Layout to work it must know where each view is positioned precisely: its X, Y, width, and height values. With intrinsic content size we can say “place this button 20 points from the top and center it horizontally” and that’s enough to form a complete layout – Auto Layout can calculate the rest based on the button’s intrinsic size.
- intrinsic content size
  - UISwitch, UIActivityIndicator, UIButton, UILabel
  - UIImageView -> The size of the image. No intrinsic size if image not set.
  - UIView, has NO intrinsic content size.
- override the intrinsic contetn size
```Swift
override var intrinsicContentSize: CGSize {
  return CGSize(width: 50, height: 20)
}
```
- content hugging / compression resistance CHCR
  - content cn shrink and grow
  -  <=50, content hugging -> how much a control should grow
  -  >=50, content compress -> how much a control shoud resist in being shrunk
  -  intrinsicContentSize constraints are optional, we adjust them through CHCR. They can be overriden with anchors.


#### Content Hugging Priorities And Content Compression Resistance Priorities
- Huggin priority comes into action when available content size is more than the total size of the content.(當可取得的大小，比實際的內容大小還要多）。notes: 系統會需要把其中的一個實際內容拉大，才能滿足實際大小。
- Huggin priority comes into action when available content size is more than the total size of the content.(當可取得的大小，比實際的內容大小還要多）。notes: 系統會需要把其中的一個實際內容拉大，才能滿足實際大小。Content Hugging Priority 較大的那個內容，會Huggin自己，其它的內容就會被expand.
- Content Compression Resistance Priority comes into action when content requires more size than the available.

#### defalut of CHCR
- By default when you create a UILabel or a UITextField in code they have a horizontal content hugging priority of 250 (.defaultLow). 

[Easier Swift Layout Priorities](https://useyourloaf.com/blog/easier-swift-layout-priorities/)
```Swift
let rawPriority = UILayoutPriority.defaultLow.rawValue
let labelPriority = UILayoutPriority(rawPriority + 1)
label.setContentHuggingPriority(labelPriority, for: .horizontal)

```
####  Operator Overload
```Swift
extension UILayoutPriority {
  static func +(lhs: UILayoutPriority, rhs: Float) -> UILayoutPriority {
    return UILayoutPriority(lhs.rawValue + rhs)
  }

  static func -(lhs: UILayoutPriority, rhs: Float) -> UILayoutPriority {
    return UILayoutPriority(lhs.rawValue - rhs)
  }
}
```
```Swift
let labelPriority = UILayoutPriority.defaultLow + 1
label.setContentHuggingPriority(.defaultLow + 1, for: .horizontal)
view.setContentCompressionResistancePriority(.defaultHigh - 1, for: .vertical)

```

#### CHCR的預設值
- setContentHugginPriority,  預設值rawValue = 250，值越高，【抗拉伸優先權】越高。 
- setContentCompressionResistancePriority, 預設值rawValue = 750， 值越高，【拉壓縮優先權】越高


#### 製作一張可彈性縮放的圖片
- 四個重點！！
  - yourImageView.translatesAutoresizingMaskIntoConstraints = false
  - yourImageView.contentMode = .scaleAspectFit
  - yourImageView.setContentHuggingPriority(UILayoutPriority(rawValue: 249), for: .vertical)
  - yourImageView.setContentCompressionResistancePriority(UILayoutPriority(rawValue: 749), for: .vertical)

```Swift
//圖片的長寛比例固定，可以依view的大小縮放。
func makeImageView(named: String) -> UIImageView {
    let view = UIImageView()
    view.translatesAutoresizingMaskIntoConstraints = false
    view.contentMode = .scaleAspectFit
    view.image = UIImage(named: named)

    // By making the image hug itself a little bit less and less resistant to being compressed
    // we allow the image to stretch and grow as required
    // CH, 250, CR, 750, 抗縮放的優先權低於標準值，表示需要縮小或放大，可以先處理它。
    view.setContentHuggingPriority(UILayoutPriority(rawValue: 249), for: .vertical)//抗拉伸的優先權低。若需要拉伸，可以先拉它。
    view.setContentCompressionResistancePriority(UILayoutPriority(rawValue: 749), for: .vertical)//抗壓縮的優先權低。若需要壓縮，可以先壓它。

    return view
}
```
##### StackView
- StackViews distribution
  - fill
  - fill equally
  - equal spacing
  - equal centering
- StackViews alignment
  - top
  - button
  - center
  - fill

- UIStackView is a container, has no instrinsic content size of its own.
- Not all distributions work the same.
- Everything inside needs to be intrinsically content sized.


#### UIStackViews Distribution - Fill
- Fills all availabe space
- Default setting
- Uses intrinsic content size(CHCR)
- If CHCR the same -  will complain

#### UIStackViews Distribution - Fill Equally
- Makes all controls the same size
- Only distribution NOT to use intrinsic content size
- Remember: intrinsic content size is an recommendation, not a requirement.
- Fill equally will break the optional intrinsic content size in order to fill equally.

#### UIStackViews Distribution - Fill Proportionally
- Maintains proportions as layout grows and shrinks.

#### UIStackViews Distribution - Equal Spacing
- Maintains equal space between each control.

#### UIStackViews Distribution - Equal Centering
- Spaces equally between center of controls.


