#### 把Array內容排序
- 使用sorted(), 就會重新排序了。
```Swift
let intArray = [2005,1997,1999,1987,1966,1254,1524]
let resortedArray = intArray.sorted()
```


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
arrayB = arrayA.shuffled()
```


#### 把array Int 存進 userDefault
- 各種存取的[例子](https://stackoverflow.com/questions/25179668/how-to-save-and-read-array-of-array-in-nsuserdefaults-in-swift)

```Swift
//save
        let selectedArray:[Int] = [20160311000003, 20161109000001, 20180426000001, 20190320000001, 20190712000003]
        let defaults = UserDefaults.standard
        defaults.set(selectedArray, forKey: "SelectedArray")
//read
        let defaults = UserDefaults.standard
        let array = defaults.array(forKey: "SelectedArray")  as? [Int] ?? [Int]()
```

#### 取得 Int array裹平均值
- use reduce()

```Swift
var intArray = [10, 15, 5, 7, 13]

//This line will take your array, intArray in this case, and reduce it starting at index number 0 and adding all the following consecutive numbers.

let sumArray = intArray.reduce(0, +)

let avgArrayValue = sumArray / intArray.count

```

#### 取得Array的 max/min
```Swift
let numbers = [1, 2, 3, 4, 5]
numbers.min() // equals 1
numbers.max() // equals 5
```

