#### 整理字串裹的字
```Swift


import Foundation

var aString : String = "0e356def2 279$%@959 44 45"

//將字串裹的空格都拿掉
aString = aString.replacingOccurrences(of: " ", with: "")

//將字串裹的文字取出，變成一個新的字串
let a  = aString.components(separatedBy: CharacterSet.decimalDigits).joined()
print(a)


//將字串裹的數字取出，變成一個新的字串
let b = aString.components(separatedBy: CharacterSet.decimalDigits.inverted).joined()
print(b)

```
