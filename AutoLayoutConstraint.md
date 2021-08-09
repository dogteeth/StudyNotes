#### 建立Constraint的三種
- storyboard
- NSLayoutAnchor
- NSLayoutConstraint


#### How it works
- leading, trailing, top, bottom
- 4 elements mus have: x, y, height, width
- setup the topAnchor constraint
```Swift

label.topAnchor.constraint(
  equalTo: view.topAnchor, //parent
  constant: 20 // 離parent的距離
  ).isActive = true

```
