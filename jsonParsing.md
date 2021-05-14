##### JSON Parsing
- 檔案所在位置，在APP裹。
- 利用Bundle.main.url取得位置進行Parsing.
- 利用以下的指令進行decode
```Swift
JSONDecoder().decode(type: Decodable.Protocol, from: Data)
```


```Swift

func versionDataParsing() {
        guard let fileLocation = Bundle.main.url(forResource: "version", withExtension: "json")
        else {return}
        do {
            let data = try Data(contentsOf: fileLocation)
            
            let safeData = try JSONDecoder().decode([VersionJSON].self, from: data)
            print(safeData[0].dataDate)
        } catch {
            print(error)
            return
        }
    }
    
```
