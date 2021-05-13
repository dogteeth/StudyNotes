##### 以當下時間做為字串：

```Swift
   //MARK: - making Time Stamp 14-digt-string

    func currentTimeStamp() -> String {
        let dateFormatter = DateFormatter()
        dateFormatter.dateFormat = "YYYYMMddHHmmss"
        let stringDate = dateFormatter.string(from: Date())
        return stringDate
    }
```
