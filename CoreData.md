##### 一些知識
- Managed Object Context（託管物件內容）: 一個暫存記憶体，裹面放著許多物件。負責管理被建立的物件，並使用core data的框架回傳。NSManagedObjectContext 的 instance。
- Managed Object Mode（託管物件模型）: 類似資料庫的schema
- Persistent Store Coordinator: NSPersistentStoreCoordinator 的 instance
- Persistent Store：SQLite

##### 在AppDelegate.swift會多出來的程式
```Swift
    // MARK: - Core Data stack

    lazy var persistentContainer: NSPersistentContainer = {
        /*
         The persistent container for the application. This implementation
         creates and returns a container, having loaded the store for the
         application to it. This property is optional since there are legitimate
         error conditions that could cause the creation of the store to fail.
        */
        let container = NSPersistentContainer(name: "OldHouseWalker_test01")
        container.loadPersistentStores(completionHandler: { (storeDescription, error) in
            if let error = error as NSError? {
                // Replace this implementation with code to handle the error appropriately.
                // fatalError() causes the application to generate a crash log and terminate. You should not use this function in a shipping application, although it may be useful during development.
                 
                /*
                 Typical reasons for an error here include:
                 * The parent directory does not exist, cannot be created, or disallows writing.
                 * The persistent store is not accessible, due to permissions or data protection when the device is locked.
                 * The device is out of space.
                 * The store could not be migrated to the current model version.
                 Check the error message to determine what the actual problem was.
                 */
                fatalError("Unresolved error \(error), \(error.userInfo)")
            }
        })
        return container
    }()

    // MARK: - Core Data Saving support

    func saveContext () {
        let context = persistentContainer.viewContext
        if context.hasChanges {
            do {
                try context.save()
            } catch {
                // Replace this implementation with code to handle the error appropriately.
                // fatalError() causes the application to generate a crash log and terminate. You should not use this function in a shipping application, although it may be useful during development.
                let nserror = error as NSError
                fatalError("Unresolved error \(nserror), \(nserror.userInfo)")
            }
        }
    }



```
##### 乾淨版

```Swift
    // MARK: - Core Data stack

    lazy var persistentContainer: NSPersistentContainer = {
     
        let container = NSPersistentContainer(name: "OldHouseWalker_test01")
        container.loadPersistentStores(completionHandler: { (storeDescription, error) in
            if let error = error as NSError? {
               
                fatalError("Unresolved error \(error), \(error.userInfo)")
            }
        })
        return container
    }()

    // MARK: - Core Data Saving support

    func saveContext () {
        let context = persistentContainer.viewContext
        if context.hasChanges {
            do {
                try context.save()
            } catch {
             
                let nserror = error as NSError
                fatalError("Unresolved error \(nserror), \(nserror.userInfo)")
            }
        }
    }

```



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
