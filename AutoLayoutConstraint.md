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
