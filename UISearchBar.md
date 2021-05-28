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



