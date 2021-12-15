#### 手動製作 CoreData
- 在 AppDelegate 加入程式
- 新增兩個CoreData File

```Swift
//Add in AppDelegate

 //MARK: - CoreData
    
    lazy var persistentContainer : NSPersistentContainer = {
        let container = NSPersistentContainer(name: "ReminderData")
        
        container.loadPersistentStores { (storeDescription, error) in
            if let error  = error as NSError? {
                fatalError("unresovled error, \(error), \(error.userInfo)")
            }
        }
        return container
    }()

```

```Swift
//Add two fileDa
// first file name: "MyDataName+CoreDataClass", second file name: "MyDataName+CoreDataProperties"


//"MyDataName+CoreDataClass"

@objc(ReminderData)
public class ReminderData :  NSManagedObject {

}
//"MyDataName+CoreDataProperties"
extension ReminderData {
    @NSManaged var title: String
    @NSManaged var isDone: Bool
    @NSManaged var dueDate: Date
}

```
