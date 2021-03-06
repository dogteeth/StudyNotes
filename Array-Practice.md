https://www.w3resource.com/swift-programming-exercises/array/index.php

#### Write a Swift program to check if 5 appears as either the first or last element in a given array of integers. The array length should be 1 or more.

- array.first, array.last
- use [logic operator "or" ](https://www.tutorialspoint.com/swift/swift_logical_operators.htm)

```Swift

let numbers1 = [1,2,3,4,5,6,7,8,9]
let numbers2 = [1,2,3,4,5,6,7,8,5]
let numbers3 = [5,2,3,4,5,6,7,8,9]
let numbers4 = [5,2,3,4,5,6,7,8,5]


func checkFiveInFirstOrLast(_ array:[Int]) -> Bool {
    /*
     !a ：不是a
     a || b ： 是a或是b
     a && b ： 同時是a也是b
     
     */
    if array.first == 5 || array.last == 5 {
        return true
    } else {
        return false
    }
    
}

print(checkFiveInFirstOrLast(numbers1))
print(checkFiveInFirstOrLast(numbers2))
print(checkFiveInFirstOrLast(numbers3))
print(checkFiveInFirstOrLast(numbers4))
```

#### Write a Swift program to check whether the first element and the last element of a given array of integers are equal. The array length must be 1 or more.

```Swift
let numbers1 = [1,2,3,4,5,6,7,8,9]
let numbers2 = [1,2,3,4,5,6,7,8,5]
let numbers3 = [5,2,3,4,5,6,7,8,9]
let numbers4 = [5,2,3,4,5,6,7,8,5]


func checkFiveInFirstOrLast(_ array:[Int]) -> Bool {
    /*
     !a ：不是a
     a || b ： 是a或是b
     a && b ： 同時是a也是b
     
     */
    if array.first ==  array.last {
        return true
    } else {
        return false
    }
    
}

print(checkFiveInFirstOrLast(numbers1))
print(checkFiveInFirstOrLast(numbers2))
print(checkFiveInFirstOrLast(numbers3))
print(checkFiveInFirstOrLast(numbers4))

```

#### Write a Swift program to test if two given arrays of integers have the same first and last element. Both arrays length must be 1 or more.

```Swift
let numbers1 = [1,2,3,4,5,6,7,8,9]
let numbers2 = [1,2,3,4,5,6,7,8,5]
let numbers3 = [5,2,3,4,5,6,7,8,9]
let numbers4 = [5,2,3,4,5,6,7,8,5]
let numbers5 = [5,2,3,7,5,6,7,8,5]


func check(arrayA:[Int], arrayB:[Int]) -> Bool {
    
    if arrayA.first == arrayB.first && arrayA.last == arrayB.last {
        return true
    } else {
        return false

    }
}

check(arrayA: numbers1, arrayB: numbers2)
check(arrayA: numbers4, arrayB: numbers5)
```
