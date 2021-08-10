#### [iPhone UIKit Size](https://developer.apple.com/library/archive/documentation/DeviceInformation/Reference/iOSDeviceCompatibility/Displays/Displays.html)
- SE: 320*568
- 6/7/8: 375*667
- 7/8Plus: 414*736
- X: 375*667


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
