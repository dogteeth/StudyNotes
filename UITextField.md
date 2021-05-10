##### 點繫出現keyboard
stimulator如果沒有自動出現keyboard, uncheck connect hardware keyboard will do the trick.

##### 輸入完畢收起keyboard
- 需要extension UITextFieldDelegate
- 設 delegate = self
- 製作 func textFieldShouldReturn

```swift
extension ViewController: UITextFieldDelegate {
    func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        textField.resignFirstResponder()
        return true
    }
}
```

##### 點擊其它地方收起keyboard

```Swift
func autoDissmissKeyboard() {
        let tap: UITapGestureRecognizer = UITapGestureRecognizer(target: self, action: #selector(dismissKeyboard))
         view.addGestureRecognizer(tap)
    }
    @objc func dismissKeyboard() {
      view.endEditing(true)
    }
```
