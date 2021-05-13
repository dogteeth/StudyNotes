##### 取得資料庫的網址

```Swift
  print(FileManager.default.urls(for: .documentDirectory, in: .userDomainMask))
```
#### UserDefault的起始設定

```Swift
 let defaults = UserDefaults.standard
    
    override func viewDidLoad() {
        super.viewDidLoad()
         
        
        //MARK: - Fisrt time launch parsing JSON to CoreData

        if defaults.bool(forKey: "First Launched") == true {
            print("not the first time, pass parsing")
            defaults.set(true, forKey: "First Launch")
            
        } else {
            print("first time launch, parsing json")
            //parsing JSON
            defaults.set(true, forKey: "First Launched")
        }

    }
```
