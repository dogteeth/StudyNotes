#### filter，判斷條件，arry裹符合條件的值納入新的array後，最後回傳。
- array裹的每一個值都依closure裹的語法判斷Bool值。true，加入回傳Array裹，false則ignore。

```Swift
let arrayOne = [1,2,3,4,5,6,7,8,9]
let arrayEven = arrayOne.filter { $0 % 2 == 0 }
print(arrayEven)
```
#### map
