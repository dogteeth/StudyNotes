#### 把Array裹，取出前面的n個數量
- 以下的用法，可以把testArray的 index位置裹的，0，1取出來。

```Swift
var test = [1, 2, 3, 4, 5, 6]
var n = 1
var test2 = test[0..<n]

```

#### Array的內容random取值
- 用shuffle()

```Swift
arrayB = arrayA.shuffle()
```


#### 把array Int 存進 userDefault

```Swift
//save
        let selectedArray:[Int] = [20160311000003, 20161109000001, 20180426000001, 20190320000001, 20190712000003]
        let defaults = UserDefaults.standard
        defaults.set(selectedArray, forKey: "SelectedArray")
//read
        let defaults = UserDefaults.standard
        let array = defaults.array(forKey: "SelectedArray")  as? [Int] ?? [Int]()
```

#### 讀取
