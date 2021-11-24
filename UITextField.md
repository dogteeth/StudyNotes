#### 需要有的功能
- 點擊輸入框，出現keyboard：好像是預設值？？
- 押了鍵盤的enter, 收起鍵盤：需要extension UITextFieldDelegate，設 delegate = self，製作 func textFieldShouldReturn
```swift
extension ViewController: UITextFieldDelegate {
    func textFieldShouldReturn(_ textField: UITextField) -> Bool {
        textField.resignFirstResponder()
        return true
    }
}
```
- 點了畫面其它的地方，收起鍵盤
- 文字有所更改時，做檢查：
```Swift
func textFieldDidChangeSelection(_ textField: UITextField) {
        yourOwnFunctionHere()
 }
```





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
