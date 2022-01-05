#### Date()
- 此方法會回傳系統當下的時間，UTC。
- UTC：為世界協調時間的縮寫為UTC，Coordinated Universal Time
- UTC、GMT（Greenwich Mean Time）兩者的標準可以。
- ＋00:00為中央標準時間
```Swift
let a = Date()
print(a)
```

- Store dates in UTC/GMT whenever you can, only use your local timezone if you’re 100% certain that your app never crosses timezones
- When representing dates as strings (i.e., for your app’s users), take in account an iPhone’s locale and calendar settings

#### DateFormatter()
- For user-visible representations of dates and times, DateFormatter provides a variety of localized presets and configuration options.
- 回傳user local date.
- 方法一
```Swift
   //MARK: - making Time Stamp 14-digt-string

    func currentTimeStamp() -> String {
        let dateFormatter = DateFormatter()
        dateFormatter.dateFormat = "YYYYMMddHHmmss"
        let stringDate = dateFormatter.string(from: Date())
        return stringDate
    }
```
- 方法二
```Swift
let currentDate = Date()
let dataFormatter = DateFormatter()
dataFormatter.locale = Locale(identifier: "zh_Hant_TW")
dataFormatter.dateFormat = "YYYY-MM-dd HH:mm:ss"
let stringDate = dataFormatter.string(from: currentDate)
```
#### [Calendar()](https://developer.apple.com/documentation/foundation/calendar)
-  A definition of the relationships between calendar units (such as eras, years, and weekdays) and absolute points in time, providing features for calculation and comparison of dates.
-  Extracting Components
-  Getting Calendar Information
-  Scanning Dates
-  Calculating Dates from Components
-  Calculating Intervals
-  Comparing Dates
-  Comparing Calendars
-  Getting AM and PM symbols
-  Getting Weekday Symbols
-  Getting Month Symbols
-  Getting Quarter Symbols
-  Getting Era Symbols

- 取得星期幾？回傳Int, 1＝星期日，
```Swift
let currentDate = Date()
let calender = Calendar(identifier: .gregorian)
let comps = (calender as NSCalendar?)?.components(NSCalendar.Unit.weekday, from: currentDate)
print(comps?.weekday ?? 0)
```

- [calendar component](https://developer.apple.com/documentation/foundation/calendar/component)
- Return Date Component. 回傳今天的一個資料（如：year, day, month, weekofYear...）
```Swift
let currentDate = Date()
let calender = Calendar(identifier: .gregorian)

let output = calender.component(.weekOfYear, from: currentDate)

print(output)
```
- Return Date Components. 回傳今天的一連串資料(放入一串array, 回傳資料）
```Swift
let currentDate = Date()
let calender = Calendar(identifier: .gregorian)
let output = calender.dateComponents([.month,.day], from: currentDate)
print(output)
```

- 取得特定月份的天數
```Swift
let currentDate = Date()
let calender = Calendar(identifier: .gregorian)

let output = calender.range(
    of: .day,
    in: .month,
    for: currentDate)?.count

print(output ?? 0)

```

#### 時區
- 取得現在的時區
```Swift
let timeZone = NSTimeZone.local
print(timeZone)
```
```Swift
let timeZone = TimeZone.current
print(timeZone)
```
-取得所有的時區代號
```Swift
let timeZone = TimeZone.knownTimeZoneIdentifiers
print(timeZone)
```
