#### CoreData ReLearn
- there is a "NSPersistentContainer" in the application delegate.(when you use CoreData as default setting)
- acess this NSPersistentContainer, using "the reference to the app delegate".
- than create a new managed object and insert it into the managed object context, using "NSManagedObject"

```Swift
func save(name:String) {
        guard let appDelegate = UIApplication.shared.delegate as? AppDelegate else {
            return
        }
        
        let managedContext =  appDelegate.persistentContainer.viewContext
        
        let entity = NSEntityDescription.entity(
            forEntityName: "Person",
            in: managedContext)!
        
        let person = NSManagedObject(
            entity: entity,
            insertInto: managedContext)
        
        person.setValue(name, forKey: "name")
        
        do {
            try managedContext.save()
            people.append(person)
        } catch let error as NSError {
            print("could not saved: \(error): \(error.userInfo)")
        }
    }
```
