#### Extension Sample
```Swift
extension ViewController: UISearchBarDelegate {
    
    func searchBarTextDidBeginEditing(_ searchBar: UISearchBar) {
        //user點擊輸入框，出現游標。
        print("searchBarTextDidBeginEditing")
        searchCancelButton.isHidden = false
    }
    
    func searchBar(_ searchBar: UISearchBar, textDidChange searchText: String) {
        //輸入文字改變
        print("textDidChange")
    }
    
    func searchBarSearchButtonClicked(_ searchBar: UISearchBar) {
        setTableViewHidden(isHidden: false)
        //點擊了鍵盤上的搜尋鍵
        print("search button clicked")
        searchBar.resignFirstResponder()
    }
    
    
}

```

#### 以下兩個method都可以收回鍵盤
- view.endEditing(true)
- yourSearchBar.  resignFirstResponder()




#### 加入 searchBar的功能
- searchBar 加到storyboard
- 建立 searchBar Outlet
- ViewController extension UISearchBarDelegate
- ViewDidLoad要設 delegate = self
- 建兩個function: searchBar-textDidChange, searchBarSearchButtonClicked

notes: 
- 在searchBar裹，"searchText"直接就是代表 輸入的text
- 要reload tableView, 不然結果出不來。

```Swift
   func searchBar(_ searchBar: UISearchBar, textDidChange searchText: String) {
        
        items = CoreDataManager.shared.searchItemsByCaseName(name: searchText)
       
        tableView.reloadData()
        
    }
    
    
    func searchBarSearchButtonClicked(_ searchBar: UISearchBar) {
        searchBar.resignFirstResponder()
    }


```



#### dismiss keyboard when tap outside the searchbar

tips from [website here:](https://www.codegrepper.com/code-examples/swift/dismiss+keyboard+when+tap+outside+swift)


```Swift
override func viewDidLoad() {
  super.viewDidLoad()
  
  let tap: UITapGestureRecognizer = UITapGestureRecognizer(target: self, action: "dismissKeyboard")
  view.addGestureRecognizer(tap)
}

@objc func dismissKeyboard() {
  view.endEditing(true)
}
```



