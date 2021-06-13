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
