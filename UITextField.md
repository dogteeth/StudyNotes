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

#### Other Version: Also works!(now deployed)
```Swift
 
    func configNotificationForKeyboard() {
        NotificationCenter.default.addObserver(self, selector: #selector(keyboardWillChange), name: UIResponder.keyboardWillShowNotification, object: nil)
       
        NotificationCenter.default.addObserver(self, selector: #selector(keyboardWillHide), name: UIResponder.keyboardWillHideNotification, object: nil)

    }
    
    @objc func keyboardWillChange(_ notification: Notification){
        let userInfo = notification.userInfo!
        let keyboardScreenEndFrame = (userInfo[UIResponder.keyboardFrameEndUserInfoKey] as! NSValue).cgRectValue
        let keyboardEndFrame = view.convert(keyboardScreenEndFrame, from: self.view)
        scrollView.contentInset = UIEdgeInsets(top: 0, left: 0, bottom: keyboardEndFrame.height, right: 0)
   
    }
    
    @objc func keyboardWillHide(_ notification: Notification){
        scrollView.contentInset = UIEdgeInsets.zero
    }
    
```
#### other version not working
[source](https://blog.jiebu-lang.com/move-view-with-keyboard-using-swift/)

```Swift
import UIKit

class ViewController: UIViewController, UITextFieldDelegate {
    
    /* 暫存輸入框元件 */
    var currentTextField: UITextField?
    /* 暫存 View 的範圍 */
    var rect: CGRect?
    
    func textFieldDidBeginEditing(_ textField: UITextField) {
        /* 開始輸入時，將輸入框實體儲存 */
        currentTextField = textField
    }
     
    override func viewDidLoad() {
        super.viewDidLoad()
        
        /* 監聽 鍵盤顯示/隱藏 事件 */
        NotificationCenter.default.addObserver(
            self,
            selector: #selector(keyboardWillShow),
            name: UIResponder.keyboardWillShowNotification,
            object: nil)
        
        NotificationCenter.default.addObserver(
            self,
            selector: #selector(keyboardWillHide),
            name: UIResponder.keyboardWillHideNotification,
            object: nil)
        
        /* 將 View 原始範圍儲存 */
        rect = view.bounds
    }
    
    /* 這個地方寫法有問題，請看文章下方補充
    override func viewDidDisappear(_ animated: Bool) {
        super.viewDidDisappear(animated)
        
        /* 移除監聽 */
        NotificationCenter.default.removeObserver(
            self,
            name: UIResponder.keyboardWillShowNotification,
            object: nil
        )
        
        NotificationCenter.default.removeObserver(
            self,
            name: UIResponder.keyboardWillHideNotification,
            object: nil
        )
    }
    */
     
    @objc func keyboardWillShow(note: NSNotification) {
        if currentTextField == nil {
            return
        }
        
        let userInfo = note.userInfo!
        /* 取得鍵盤尺寸 */
        let keyboard = (userInfo[UIResponder.keyboardFrameEndUserInfoKey] as! NSValue).cgRectValue.size
        let duration = userInfo[UIResponder.keyboardAnimationDurationUserInfoKey] as! Double
        /* 取得焦點輸入框的位置 */
        let origin = (currentTextField?.frame.origin)!
        /* 取得焦點輸入框的高度 */
        let height = (currentTextField?.frame.size.height)!
        /* 計算輸入框最底部Y座標，原Y座標為上方位置，需要加上高度 */
        let targetY = origin.y + height
        /* 計算扣除鍵盤高度後的可視高度 */
        let visibleRectWithoutKeyboard = self.view.bounds.size.height - keyboard.height
        
        /* 如果輸入框Y座標在可視高度外，表示鍵盤已擋住輸入框 */
        if targetY >= visibleRectWithoutKeyboard {
            var rect = self.rect!
            /* 計算上移距離，若想要鍵盤貼齊輸入框底部，可將 + 5 部分移除 */
            rect.origin.y -= (targetY - visibleRectWithoutKeyboard) + 5
            
            UIView.animate(
                withDuration: duration,
                animations: { () -> Void in
                    self.view.frame = rect
                }
            )
        }
    }
     
    @objc func keyboardWillHide(note: NSNotification) {
        /* 鍵盤隱藏時將畫面下移回原樣 */
        let keyboardAnimationDetail = note.userInfo as! [String: AnyObject]
        let duration = TimeInterval(truncating: keyboardAnimationDetail[UIResponder.keyboardAnimationDurationUserInfoKey]! as! NSNumber)
        
        UIView.animate(
            withDuration: duration,
            animations: { () -> Void in
                self.view.frame = self.view.frame.offsetBy(dx: 0, dy: -self.view.frame.origin.y)
            }
        )
    }
}
```
