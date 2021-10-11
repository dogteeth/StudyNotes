#### Use Protocol to pass values between views
[video](https://www.youtube.com/watch?v=DBWu6TnhLeY)

- 在secondView，class之前設定 protocol
- 在viewDidLoad將 delegate 實例化
- action的地方，進行protocol的資料設定
- 在mainView的地方，像tableView一樣，設extension, 同時設delegate=self，即完成value的passing.

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
