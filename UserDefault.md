

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
