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
