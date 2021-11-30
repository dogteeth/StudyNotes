#### Protocol Delegate Implement
[source](https://stackoverflow.com/questions/24099230/delegates-in-swift/33549729)

- Step 1: Make a protocol in the UIViewController that you will be removing/will be sending the data.
- Step 2: Declare the delegate in the sending class (i.e. UIViewcontroller)
- Step 3: Use the delegate in a class method to send the data to the receiving method, which is any method that adopts the protocol.
- Step 4: Adopt the protocol in the receiving class
- Step 5: Implement the delegate method
- Step 6: Set the delegate in the prepareForSegue:




#### Use Protocol to pass values between views
[video](https://www.youtube.com/watch?v=DBWu6TnhLeY)

- 在secondView，class之前設定 protocol
- 在viewDidLoad將 delegate 實例化
- action的地方，進行protocol的資料設定
- 在mainView的地方，像tableView一樣，設extension, 同時設delegate=self，即完成value的passing.


#### 重點
- secondView在mainView必需被create分身，同時加入delegate = self (這段好難...)

```Swift
//secondView
//before class
protocol SideMenuViewControllerDelegate {
    func selectedCell(_ row: Int)
    func printSelectedCellString( _ labelString:String)
}

//in viewDidLoad
var delegate: SideMenuViewControllerDelegate?

//in action 
delegate?.selectedCell(indexPath.row)
delegate?.printSelectedCellString(dummyArray[indexPath.row])
```

```Swift

//before viewDidLoad
let sidbarVC = SidebarVC()


//add extension to the class
extension ViewController: SideMenuViewControllerDelegate {
    
    func printSelectedCellString(_ labelString: String) {
        
        mainLabel.text  = labelString
    }
    
   
    func selectedCell(_ row: Int) {
        switch row {
        case 0:
            print("tap 0")
        case 1:
            print("tap 1")
        default:
            break
        }
        sidbarVC.view.removeFromSuperview()
        isOpen = false
        
    }

    
}

```
