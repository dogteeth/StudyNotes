dissmiss keyboard when tap outside the searchbar
from [here:](https://www.codegrepper.com/code-examples/swift/dismiss+keyboard+when+tap+outside+swift)


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
