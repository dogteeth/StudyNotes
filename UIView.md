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
