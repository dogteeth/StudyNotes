##### 以當下時間做為字串：

```Swift
func currentTimeStamp() -> String {
    dateFormatter.dateFormat = "YYYYMMddHHmm"
    let stringDate = dateFormatter.string(from: Date())
    return stringDate
}
```
