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
