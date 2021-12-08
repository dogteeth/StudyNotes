##### 一些知識
- Managed Object Context（託管物件內容）: 一個暫存記憶体，裹面放著許多物件。負責管理被建立的物件，並使用core data的框架回傳。NSManagedObjectContext 的 instance。
- Managed Object Mode（託管物件模型）: 類似資料庫的schema
- Persistent Store Coordinator: NSPersistentStoreCoordinator 的 instance
- Persistent Store：SQLite
- CoreData Entity -> 想成是表頭
- CoreData Attributes -> 表頭裹的每一個欄位
- CoreData NSManagedObject -> 表頭下的每一列（滿足表頭定義的一行資料），都是一個CoreData Object

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

#### CoreData Singleton的製作：
CoreDataManager.shared.dataFunction()

```Swift

   //加了static之後的內容，變成了class本身。instance是不可以使用的。
    static let shared = CoreDataManager()
    
    //NSPersistentStoreDescription
    //NSPersistenetContainer
    //宣告的形式 -> persistentContainer: () = {}()
    let persistentContainer : NSPersistentContainer = {
        let container = NSPersistentContainer(name: "OldHouseWalkingV05")
        container.loadPersistentStores { storeDescription, error in
            if let error = error {
                fatalError("Loding Failed \(error)")
            }
        }
        return container
    }()
    

```

- 依條件尋找Core Data

```Swift

 func fetchItemByCaseName(name caseName:String) -> Item? {
        let context = persistentContainer.viewContext
        let fetchRequest = NSFetchRequest<Item>(entityName: "Item")
        
        fetchRequest.predicate = NSPredicate(format: "caseName == %@", caseName)
        
        do {
            let itemsFetched = try context.fetch(fetchRequest)
            return itemsFetched.first
            
        } catch let fetchError {
            print("Failed to fetch companies :\(fetchError)")
        }
        return nil
    }
    
```
- NSPredicate的條件，int與string都有不同。

```Swift
//String
fetchRequest.predicate = NSPredicate(format: "caseName == %@", caseName)
//Int
fetchRequest.predicate = NSPredicate(format: "caseId == \(id)")
```


#### CoreData存入Array String

<img width="967" alt="001" src="https://user-images.githubusercontent.com/18608853/135399202-59707971-d0ca-4022-b7bb-9cc7cf8eda80.png">

- 加入：NSSecureUnarchiveFromData : set NSSecureUnarchiveFromData to Value Transformer (it was renamed to just "Transformer"). Otherwise, you may get this runtime warning: 'NSKeyedUnarchiveFromData' should not be used to for un-archiving and will be removed in a future release

- when use transformable, with custom class, transformer should use "NSSecureUnarchiveFromData".

- another reference [link](https://www.lexicon.com.au/blog/how-to-save-an-array-of-custom-data-types-in-core-data-with-transformable-and-nssecurecoding-in-ios)



#### CoreData Warning
- Multiple NSEntityDescriptions Claim NSManagedObject Subclass
- the solution:  [link](https://github.com/drewmccormack/ensembles/issues/275)
```Swift

import CoreData
public extension NSManagedObject {

    convenience init(context: NSManagedObjectContext) {
        let name = String(describing: type(of: self))
        let entity = NSEntityDescription.entity(forEntityName: name, in: context)!
        self.init(entity: entity, insertInto: context)
    }

}


```
#### CoreData CRUD
- create, read, update, delete
- delete object
    - get the context
    - use .delete function, with object you want to delete
(超簡單...)

```Swift
   func deletePlayer(deletePlayer: Player) {
        let context = persistentContainer.viewContext
        do {
            context.delete(deletePlayer)            
            try context.save()
            
        } catch {
            print("deletePlayer :error")
        }
    }
```
- read all data
    - get the context
    - set NSFetchRequest
    - set NSSortDescriptor
    - combine NSSortDescriptor with NSFetchRequest
    - use .fetch to fetch data
```Swift


func getAllPlayers() -> [Player]? {
        // get the context
        let context = persistentContainer.viewContext
        // set NSFetchRequest
        let fetchRequest = NSFetchRequest<Player>(entityName: "Player")
        
        // set NSSortDescriptor
        let sortDescriptor = NSSortDescriptor(key: "playerName", ascending: true)
        let sortDescriptors = [sortDescriptor]
        
        //combine NSSortDescriptor with NSFetchRequest
        fetchRequest.sortDescriptors = sortDescriptors
       
        do {
            //use .fetch to fetch data
            let playerFetched = try context.fetch(fetchRequest)
            return playerFetched
            
        } catch {
            print(error)
        }
        return nil
        
    }

```
