##### 取得資料庫的網址

```Swift
  print(FileManager.default.urls(for: .documentDirectory, in: .userDomainMask))
```
#### UserDefault的起始設定

> https://developer.apple.com/documentation/foundation/userdefaults/1416388-bool
> func bool(forKey defaultName: String) -> Bool
> The Boolean value associated with the specified key. If the specified key doesn‘t exist, this method returns false.
> UsersDefaults: An interface to the user’s defaults database, where you store key-value pairs persistently across launches of your app.

```Swift
 let defaults = UserDefaults.standard
    
    override func viewDidLoad() {
        super.viewDidLoad()
         
        
        //MARK: - Fisrt time launch parsing JSON to CoreData

        if defaults.bool(forKey: "First Launched") == true {
            print("not the first time, pass parsing")
            //defaults.set(true, forKey: "First Launch") 這行是多餘的。
            
        } else {
            print("first time launch, parsing json")
            //parsing JSON
            defaults.set(true, forKey: "First Launched")
        }

    }
```
