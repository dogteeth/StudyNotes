
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

- 另一個例子。
```Swift
   cell.tapGoogleAction = { _ in
       let text  = self.itemPassing?.caseName ?? "main"
       let url = "https://www.google.co.in/search?q=" + text
       if let urlString = URL(string: url.urlEncoded()) {
              let config = SFSafariViewController.Configuration()
              config.entersReaderIfAvailable = true
              let vc = SFSafariViewController(url: urlString, configuration: config)
              self.present(vc, animated: true)
        }
    }
```



#### 讓cell在往上滾動時，出現fade out的功能。

```swift
   override func scrollViewDidScroll(_ scrollView: UIScrollView) {
        for cell in tableView.visibleCells as [UITableViewCell] {
            let point = tableView.convert(cell.center, to: tableView.superview)
            cell.alpha = ((point.y * 100) / tableView.bounds.maxY) / 100
        }
    }
```

#### 刪除row

```Swift
 override func tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, forRowAt indexPath: IndexPath) {
        
        if editingStyle == .delete {
            let safeItem = items?[indexPath.row] 
            items?.remove(at: indexPath.row)
            tableView.deleteRows(at: [indexPath], with: .fade)
            
            CoreDataManager.shared.deletingReadingTimeStamp(item: safeItem)
        }
    }
```
