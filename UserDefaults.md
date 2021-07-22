#### 利用UserDefaults做App第一次使用的處理。

- 先宣告 defaults

```Swift
    let defaults = UserDefaults.standard

```
- 在viewDidLoad的地方，處理。
- UserDefaults的 bool 預設值為false, 找不到值時，也是以false來處理。故，第一次launch時，即可以依false先執行目標物後，再改成true. 第二次再後就不會再執行了。

```Swift

        
        // if bool == true, parsing JSON to CoreData
        if defaults.bool(forKey: "First Launched") == true {
            //defaults.set(true, forKey: "First Launch")
            print("not the first time launched , parsing PASSED!")
            
        } else {
            print("first time launch, parsing json")
            defaults.set(true, forKey: "First Launched")
            caseJSONParsing()
            
        }

```


#### 利用UserDefaults記錄特定功能的開關
- 宣告UserDefaults, 開關的變數
```Swift
    let defaults = UserDefaults.standard
    var isClose:Bool?
```
- 在viewDidLoad的地方，進行進設定
```Swift
 override func viewDidLoad() {
        super.viewDidLoad()
        
        isClose = defaults.bool(forKey: "caseRecommendationIsOpen") //UserDefaults的bool的預設值是false
```
- 在function內，進行var isClose的操作，每次操作完都回存UserDefaults，下次再進入app，即可取得最後變動的UserDefaults

```Swift
 @IBAction func caseRecommendBTNPressed(_ sender: UIButton) {
        isClose = !(isClose ?? false)
        defaults.setValue(isClose, forKey: "caseRecommendationIsOpen")
        updateCaseRecommendationView(isClose: isClose ?? false)
    }
```

#### 利用UserDefaults紀錄使用字形大小
- 宣告UserDefaults
```Swift
    let defaults = UserDefaults.standard
```
- viewDidLoad的地方，取UserDefault的值。
```Swift
 override func viewDidLoad() {
        super.viewDidLoad()
        
        let userDefaultTextFontSize = defaults.integer(forKey: "readerModeFontSize")
        
        stepper.value = Double(userDefaultTextFontSize)
        stepper.maximumValue = 70
        stepper.minimumValue = 18
        
        textView.text = readerModeString
        textView.font = textView.font?.withSize(CGFloat(userDefaultTextFontSize))
        
    }
```
- 在function的地方做操作，並回存UserDefaults
```Swift
 @IBAction func fontSizeBTN(_ sender: UIStepper) {
        
        defaults.setValue(Int(sender.value), forKey: "readerModeFontSize")
        
        textView.font = textView.font?.withSize(CGFloat(sender.value))
    }
```
