#### 取得時間印章
```Swift
    static func currentTimeStamp() -> String {
        let dateFormatter = DateFormatter()
        dateFormatter.dateFormat = "YYYYMMddHHmmss"
        let stringDate = dateFormatter.string(from: Date())
        return stringDate
    }
```
