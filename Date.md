##### 以當下時間做為字串：

```Swift
func currentTimeStamp() -> String {
    let dateFormatter = DateFormatter()
    dateFormatter.dateFormat = "YYYYMMddHHmm"
    let stringDate = dateFormatter.string(from: Date())
    return stringDate
}
```
