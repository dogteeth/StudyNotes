
##### cell押了不要有任何動畫。
- 此語法，cell還是可以選，只是不會有任何的動畫。

```swift
cell.selectionStyle = .none
```

#### 在Cell裹的Button的設計
- 在 cell的 ViewController裹，要做closure的設計。
```Swift

var tapAction : ((UITableViewCell)->Void)?

```
- 在 cell的 ViewController裹的button, 押了後，call action。

```Swift
  @IBAction func bookmarkPressed(_ sender: UIButton) {
        tapAction?(self)
    }
```
- 在 TableViewController的 cellForRow 的 function裹，再進行這個action的定義。

```Swift
  cell.tapAction = { cell in
    self.isBookmarkedBool = !self.isBookmarkedBool
    self.updateBookmarkCoredata(to: self.isBookmarkedBool)
    tableView.reloadData()
  }
```
