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
- 判斷keyboard的高度,輸入表格進行scroll





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
// function One
func autoDissmissKeyboard() {
        let tap: UITapGestureRecognizer = UITapGestureRecognizer(target: self, action: #selector(dismissKeyboard))
         view.addGestureRecognizer(tap)
    }

// function Two
@objc func dismissKeyboard() {
      view.endEditing(true)
    }
```

#### UITextField And Keyboard show & hide
[source](https://www.youtube.com/watch?v=kD6vw0hp5WU&t=682)
- textField放進scrollView
- 當keyboard出現時，調整 UIScrollView contentInset到keyboard的上方。
- listen two event, 1. keyboard will show, 2. keyboard will hide
- start listening when viewWillAppear, and stop listening when viewWillDisappear
- use "keyboard will show", to get the height of the keyboard
- use the height to adjust UIScrollView contentInset.
- handle the size of scroll indicator use the property called "UIScorllView scrollIndicatorInsets"
- when keyboard will disappear, reset "UIScrollView contentInset, scrollIndicatorInsets" and stop listening.


#### Best Solution
[source](https://www.youtube.com/watch?v=D3sxanj3vd8)
[source2](https://stackoverflow.com/questions/29903893/swift-get-keyboard-input-as-the-user-is-typing)

```Swift
    //MARK: - keyboard and textField
    
    func addNotificationForKeyboard() {
        NotificationCenter.default.addObserver(self, selector: #selector(keyboardWillChange), name: UIResponder.keyboardWillChangeFrameNotification, object: nil)
        
        NotificationCenter.default.addObserver(self, selector: #selector(keyboardWillHide), name: UIResponder.keyboardWillHideNotification, object: nil)
    }
    
    @objc func keyboardWillChange(_ notification: Notification){
        let userInfo = notification.userInfo!
        let keyboardScreenEndFrame = (userInfo[UIResponder.keyboardFrameEndUserInfoKey] as! NSValue).cgRectValue
        let keyboardEndFrame = self.convert(keyboardScreenEndFrame, from: self)
        scrollView.contentInset = UIEdgeInsets(top: 0, left: 0, bottom: keyboardEndFrame.height, right: 0)
    }
    
    @objc func keyboardWillHide(_ notification: Notification){
        scrollView.contentInset = UIEdgeInsets.zero
    }

```
