

This is a closure, that has no function parameters, and return nothing.

```swift
() -> ()

() -> Void

```

或是這個。 a  parameter, return nothing


```swift
{ (name:String) in
  print("hello! \(name)")
}

(String) -> Void

```

closure是一個自帶變數，可供user呼叫後再指定操作方式的 function.
以下這個function的設計是

sayHello有兩個變數，一個是 string, 一個是closure。 它拿到變數後，會先把它變成大寫。然後再傳給closure去處理。
呼叫sayHello這個function時，系統會自動要求，變數要放什麼？closure要做什麼事？
在closure的地方，自己設變數名，還有變數處理的methods.變數名，在執行的時候，自動就會由sayHello的變數傳入。

```swift
func sayHello(to name: String, finallySayIt: (String) -> Void) {
  let newName = name.uppercased()
  finallySayIt(newName)
}
```

closure本身也可以是 function回傳的變數。
以下這個sayIt function, 呼叫時，不需要任何變數，它會回傳一個closure: (String)->()。而這個closure，接受一個String之後，做處理。

```swift
func sayIt() -> (String)-> Void {
  return { (nama) in
   print("Hello \(name)")
  }
}
```

呼叫這個function時，要用這個方式

```swift

//這不會work
sayIt()

//這可以。
sayIt()("Paul")

//或是這樣也可以

let greetings = sayIt()
greeting("Paul")


```





