#### filter：回傳判斷條件為yes的新Array
- array裹的每一個值都依closure裹的語法判斷Bool值。true，加入回傳Array裹，false則ignore。

```Swift
let arrayOne = [1,2,3,4,5,6,7,8,9]
let arrayEven = arrayOne.filter { $0 % 2 == 0 }
print(arrayEven)
```
#### map


#### indices: 回傳 array index的 type為Int的range
- index 的複數，叫 "indices"
