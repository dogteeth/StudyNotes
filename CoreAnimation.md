#### Defination
- What is Animation: A change in a value or state over time.
- Start Value + End Value + Time
- Figure out which contraints control the view?
- "It contains every constraints held by a view": Constraints are held by the closest view, that contains both items in the constraint.
- Contraints that are held by a view, don't constitute an exhaustive list of constraints that affect a view.
- Every constraint that affects a view, is listed in the Size Inspector.
- Constraints that a view holds are listed  on the left in the document outline.
- A contraint between a sub view and its super view is held by the super view.
- A constraint by two sub views is held by the super view of both.

#### To Animate

- animate有四種，以下為其中一種。
```Swift

UIView.animate(
        withDuration: 1 / 3 , 
        delay: 0 , 
        options: .curveEaseIn , 
        animations: {
                self.view.layoutIfNeeded()
        },
        completion: 
        )
```
- 重點在 animations: { self.view.layoutIfNeeded()}, 意指：以這個時間內，重新繪制layoutConstraints
- 在trigger animations的地方，設定新的layoutConstraints, 然後加上 UIView.animate後，在這一句的程式裹，即會出現動畫的效果。若有transform的需要，也可以這裹加上。如：menuButton.transform = .init(rotationAngle: self.menuIsOpen ? .pi / 4 : 0)  -》         把加號的button旋轉，變成X號。
```Swift
    UIView.animate(withDuration: 1 / 3, delay: 0, options: .curveEaseIn, animations: {
            self.menuButton.transform = .init(rotationAngle: self.menuIsOpen ? .pi / 4 : 0)
            self.view.layoutIfNeeded()
        })

```




#### class CABasicAnimation : CAPropertyAnimation
- An object that provides basic, single-keyframe animation capabilities for a layer property.
- keyPath:  [keyPath support](https://developer.apple.com/library/archive/documentation/Cocoa/Conceptual/CoreAnimation_guide/Key-ValueCodingExtensions/Key-ValueCodingExtensions.html) 
  - opacity — 不透明度
  - backgroundColor — 背景顏色
  - position — 座標移動
  - transform — 變形效果


- UIView, 下方有個 CALayer, CALayer是所有動畫發生的地方。如 cornerRadius, shadows, animations
- Animation,有兩個layer要處理，1. model layer(the shape looks like now), 2.presentation layer(the shape looks like while animating)

#### 動態性取得iphone screen的大小，做為 animation的值
```Swift
override func viewDidAppear(_ animated: Bool) {
        let wid = view.bounds.width
        let hei = view.bounds.height
        print("width = \(wid), height = \(hei)")}

```

#### textField做動畫
- myView.frame.origin.y -= 50 // 將myView將自身的y軸，減少50

```Swift
 func closeSearchBar(){
        
        UIView.animate(withDuration: 0.5) {
            self.searchCancelButton.frame.origin.y -= 50
            self.searchBar.frame.origin.y -= 50
        } completion: { _ in
            self.searchBar.isHidden = true
            self.searchCancelButton.isHidden = true
        }
        
    }
```

- 改變imageView的alpha值

```Swift
   func closeNoResutlsAnimated() {
        UIView.animate(withDuration: 0.1) {
            self.noResultsStack.alpha = 0
        } completion: { _ in
            self.noResultsStack.alpha = 1

            self.noResultsStack.isHidden = true
            self.cancelButton.isHidden = true
            self.tableView.isHidden = true
        }
    }
```
