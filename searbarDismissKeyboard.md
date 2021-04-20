dissmiss keyboard when tap outside the searchbar


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
