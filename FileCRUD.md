#### What is Bundle

On Apple’s platforms, apps are distributed as bundles, which means that in order to access internal files that we’ve included (or bundled) within our own app, we’ll first need to resolve their actual URLs by searching for them within our app’s main bundle.
That main bundle can be accessed using Bundle.main, which lets us retrieve any resource file that was included within our main app target


#### 在JSON file裹寫入資料（over write)
```Swift
func writeJSON() {
        let jsonString = "{\"location\": \"the moon\"}"
        
        guard let fileLocation = Bundle.main.url(forResource: "myJsonString", withExtension: "json")
        else {return}
        

        do {
            try jsonString.write(to: fileLocation,
                                 atomically: true,
                                 encoding: .utf8)
            print("write succeed")

        }  catch {
            print(error.localizedDescription)
        }

    }
    
```

#### Get the file size
```Swift
func getJSONSize() {
        guard let filePath = Bundle.main.path(forResource: "myJsonString", ofType: "json")
        else {return}
        
        var fileSize : UInt64
        
        do {
            let attr = try FileManager.default.attributesOfItem(atPath: filePath)
                fileSize = attr[FileAttributeKey.size] as! UInt64
            print(fileSize)
            
            labelString.text = String(fileSize)
            
        } catch {
             print("Error: \(error)")

        }
    }
```

#### delete file
- 取得 filelocation, 用 Bundle.main.url
- removeItem(at:  _ ) 刪除檔案

```Swift

 guard let fileLocation = Bundle.main.url(forResource: "myJsonString", withExtension: "json")
        else {return}
        
    
        do {
             try FileManager.default.removeItem(at: fileLocation)
            
        } catch {
             print("Error: \(error)")

        }

```
