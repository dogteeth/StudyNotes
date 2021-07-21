#### 讓view的上面左右兩角呈㘣形
```Swift
  func roundCorners(inputView:UIView, cornerRadius: Double) {

        inputView.layer.cornerRadius = CGFloat(cornerRadius)

        inputView.clipsToBounds = true

        inputView.layer.maskedCorners = [.layerMinXMinYCorner, .layerMaxXMinYCorner]

    }
```

[資料來源](https://www.appcoda.com.tw/rounded-corners-uiview/)
