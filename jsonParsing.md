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


```swift
func caseJSONParsing() {
        
        guard let fileLocation = Bundle.main.url(forResource: "0-600json", withExtension: "json")
        else {return}
        
        do {
            let data = try Data(contentsOf: fileLocation)
            
            let safeData = try JSONDecoder().decode([CaseJSON].self, from: data)
            
            for n in safeData {
                let newItem = Item(context: context)
                
                
                newItem.caseId = Int64(n.caseId)
                newItem.caseName = n.caseName
                newItem.tagline = n.tagline
                newItem.assetsClassifyName = n.assetsClassifyName
                newItem.functionCategoryName = n.functionCategoryName
                newItem.firstRecordDynastyName = n.firstRecordDynastyName
                newItem.firstRecordEmperorName = n.firstRecordEmperorName
                newItem.firstRecordYears = Int64(n.firstRecordYears ?? 0)
                
                //
                newItem.pastHistory = n.pastHistory
                newItem.buildingFeatures = n.buildingFeatures
                newItem.architectArtist = n.architectArtist
                
                //
                newItem.registerDate = n.registerDate
                newItem.belongCity = n.belongCity
                newItem.belongCityArea = n.belongCity
                newItem.belongAddress = n.belongAddress
                newItem.govInstitutionName = n.govInstitutionName
                newItem.govInstitution = n.govInstitution
                newItem.govDeptName = n.govDeptName
                
                //
                newItem.representImage = n.representImage
                newItem.imageSourceLink = n.imageSourceLink
                
                //
                newItem.longitude = n.longitude
                newItem.latitude = n.latitude
                
                
                try context.save()
            }
        } catch {
            print(error)
            return
        }
    }
    
  ```
