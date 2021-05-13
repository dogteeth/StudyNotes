```Swift

let fileLocation = Bundle.main.url(forResource: "blahblahblah", withExtension: "json")

 
        do {
            let data = try Data(contentsOf: fileLocation)
        } catch {
            print(error)
            return
        }
```
