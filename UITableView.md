#### datasource 和 delegate的差別
- delegate: 用來控制 UI event,像是選擇 table cell 後該做什麼動作.
- datasource: 顯示 table cell 內的資料(datasource).

#### 取得特定的cell

```swift
let cell = tableView.cellForRow(at: indexPath)
```

##### tableView drag and drop
- set  tableView.dragInteractionEnabled = true
- set  tableView.dragDelegate = self
- implement two functions:
  - 1.tableView(_:moveRowAt:to:)
  - 2.tableView(_:itemsForBeginning:at:) 
```Swift

//UITableViewDataSource
    func tableView(_ tableView: UITableView, moveRowAt sourceIndexPath: IndexPath, to destinationIndexPath: IndexPath) {
        guard sourceIndexPath != destinationIndexPath else {
            return
        }
        
        let item = dummyNameArray[sourceIndexPath.row]
        
        if sourceIndexPath.row < destinationIndexPath.row {
            dummyNameArray.insert(item, at: destinationIndexPath.row + 1)
            dummyNameArray.remove(at: sourceIndexPath.row)
        } else {
            dummyNameArray.remove(at: sourceIndexPath.row)
            dummyNameArray.insert(item, at: destinationIndexPath.row)
        }
        
        //print the result
        dummyNameArray.forEach {
            print($0)
        }
        print()
    }

//UITableViewDragDelegate
     func tableView(_ tableView: UITableView, itemsForBeginning session: UIDragSession, at indexPath: IndexPath) -> [UIDragItem] {
        return [UIDragItem(itemProvider: NSItemProvider())]
    }
```



#### tableView 選取多個 cell
```Swift

  func tableView(_ tableView: UITableView, willDeselectRowAt indexPath: IndexPath) -> IndexPath? {
     return nil
     
     }

```

#### tableView 自動選取 cell 
```Swift
let path = IndexPath(row: atRow, section: 0)
tableView.selectRow(at: path, animated: false, scrollPosition: .none)
```
#### tableView 自動roll到 cell 
```Swift
let indexPathRow = IndexPath(row: rowIndex, section: 0)
tableView.scrollToRow(at: indexPathRow, at: .top, animated: true)
```
#### tableView設計 header in section
- tableView:viewForHeaderInSection, 這個return UIView。所以可以直接可以把設計好的cell放進來宣告，做為輸出。cell也是一個UIView
- tableView的高度，可以用tableView:heightForHeaderInSection

```Swift
 func tableView(_ tableView: UITableView, viewForHeaderInSection section: Int) -> UIView? {
        
        let cell = tableView.dequeueReusableCell(withIdentifier: TimeTable1TVC.identifier) as! TimeTable1TVC
        
        cell.tabArray = tabs
        cell.setNeedsLayout()
        return cell
    }
    
    func tableView(_ tableView: UITableView, heightForHeaderInSection section: Int) -> CGFloat {
        return normalHeight
        
    }
```

#### tableHeaderView 是另外一種HeaderView
- header有兩種。一種是整個table header的，另外一種是section header
- table header 沒有現成的function，直接在viewDidLoad或其它的func裹宣告。
- tableView.tableHeaderView = someView, 用這句來宣告。someView，可以是任何設定好的view。

```Swift
 let cell = tableView.dequeueReusableCell(withIdentifier: TimeTable1TVC.identifier) as! TimeTable1TVC
        let header = cell
        tableView.tableHeaderView = header
        cell.tabArray = tabs
```

- 另外一種sample
```Swift
//tableView加入 header
        let cell = tableView.dequeueReusableCell(withIdentifier: CellIdentifier.HeaderImageTVC) as! HeaderImageTVC
        cell.headerImageView.image = UIImage(named: String(caseId))
        let header = cell
        tableView.tableHeaderView = header
        tableView.tableHeaderView?.frame.size = CGSize(width: view.frame.width, height: 300)
```



- table header的設計，可以tableView:willDisplayHeaderView這個function裹，做view的相關設計。
```Swift
override func tableView(tableView: UITableView, willDisplayHeaderView view: UIView, forSection section: Int) 
{
    // Background view is at index 0, content view at index 1
    if let bgView = view.subviews[0] as? UIView
    {
        // do your stuff
    }

    view.layer.borderColor = UIColor.magentaColor().CGColor
    view.layer.borderWidth = 1
}

```

#### tableView不要有線
```Swift
tableView.separatorStyle = .none
```

#### Cell的高度
- 在viewDidLoad加入設定。
```Swift
tableView.rowHeight = UITableView.automaticDimension
```


##### cell押了不要有任何動畫。
- 此語法，cell還是可以選，只是不會有任何的動畫。

```swift
cell.selectionStyle = .none
```

#### 在Cell裹的Button的設計
notes:
1. 以closure做一個var, ex.   var toDoSomething : ((UITableViewCell) -> Void)?
2. button押了的程式，呼叫這個clourse, ex. toDoSomething?(self)
3. ViewController裹定義這個var的內容物。 ex. cell.toDoSomething = { cell in //something to do... }

- 在 cell的 ViewController裹，要做closure的設計。
```Swift

var tapAction : ((UITableViewCell)->Void)?

```
- 在 cell的 ViewController裹的button, 押了後，call action。

```Swift
  @IBAction func bookmarkPressed(_ sender: UIButton) {
        tapAction?(self)
    }
```
- 在 TableViewController的 cellForRow 的 function裹，再進行這個action的定義。

```Swift
  cell.tapAction = { cell in
    self.isBookmarkedBool = !self.isBookmarkedBool
    self.updateBookmarkCoredata(to: self.isBookmarkedBool)
    tableView.reloadData()
  }
```

- 另一個例子。
```Swift
   cell.tapGoogleAction = { _ in
       let text  = self.itemPassing?.caseName ?? "main"
       let url = "https://www.google.co.in/search?q=" + text
       if let urlString = URL(string: url.urlEncoded()) {
              let config = SFSafariViewController.Configuration()
              config.entersReaderIfAvailable = true
              let vc = SFSafariViewController(url: urlString, configuration: config)
              self.present(vc, animated: true)
        }
    }
```



#### 讓cell在往上滾動時，出現fade out的功能。

```swift
   override func scrollViewDidScroll(_ scrollView: UIScrollView) {
        for cell in tableView.visibleCells as [UITableViewCell] {
            let point = tableView.convert(cell.center, to: tableView.superview)
            cell.alpha = ((point.y * 100) / tableView.bounds.maxY) / 100
        }
    }
```



#### [刪除row](https://stackoverflow.com/questions/29886642/hide-uitableview-cell)

```Swift
 override func tableView(_ tableView: UITableView, commit editingStyle: UITableViewCell.EditingStyle, forRowAt indexPath: IndexPath) {
        
        if editingStyle == .delete {
            let safeItem = items?[indexPath.row] 
            items?.remove(at: indexPath.row)
            tableView.deleteRows(at: [indexPath], with: .fade)
            
            CoreDataManager.shared.deletingReadingTimeStamp(item: safeItem)
        }
    }
```


#### hide the cell
[連結](https://stackoverflow.com/questions/29886642/hide-uitableview-cell)
- hide the cell
- set the height of the row to zero

```Swift

func tableView(tableView: UITableView, 
               cellForRowAtIndexPath indexPath: NSIndexPath) -> UITableViewCell {

   let cell = tableView.dequeueReusableCellWithIdentifier("Cell", forIndexPath: indexPath)

   if indexPath.row == 1 {
       cell?.hidden = true
   } else {
       cell?.hidden = false
   }
   return cell      
}


func tableView(tableView: UITableView, heightForRowAtIndexPath indexPath: NSIndexPath) -> CGFloat {

    var rowHeight:CGFloat = 0.0

    if(indexPath.row == 1){
        rowHeight = 0.0
    } else {
        rowHeight = 55.0    //or whatever you like
    }
    return rowHeight
}


```

#### 押了cell 改變背景
- 在 cell的 controller裹做以下的程式
```Swift
  override func setSelected(_ selected: Bool, animated: Bool) {
        super.setSelected(selected, animated: animated)
        if selected {
            UIView.animate(withDuration: 0.8, animations: {
                self.backgroundColor = .red
            })
            isExpanded = !isExpanded
            changeHeight?(self)
           } else {
               self.backgroundColor = .white
            isExpanded = !isExpanded
            changeHeight?(self)
           }
        
    }
```

#### 押了改變cell高度 
- 宣告變數

```Swift
let normalHeight:CGFloat = 50
let expandHeight:CGFloat = 200
```

- 加入判斷程式，與更新程式 
```Swift

 override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        tableView.beginUpdates()
        tableView.endUpdates()
        
 }

 override func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        
        if tableView.indexPathForSelectedRow?.row == indexPath.row {
            return expandHeight;
        } else {
            return normalHeight;
        }
 }
    
```


#### tap to expand, tap again to close
```Swift
 var isExpanded:Bool = false
 var selectedRow = -1
 
 override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        if selectedRow == -1 {
            print("it's the frist")
            selectedRow = indexPath.row
            isExpanded = true
        } else if selectedRow == indexPath.row {
             print("you tapped the same cell")
            isExpanded = !isExpanded
        } else {
            isExpanded = true
            print("you changed the cell")
        }
        print(indexPath.row)
        selectedRow = indexPath.row
        
        tableView.beginUpdates()
        tableView.endUpdates()
        
    }
    
override func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        
        if tableView.indexPathForSelectedRow?.row == indexPath.row && isExpanded {
            return expandHeight;
        }
        
        return normalHeight;
        
    }

```
- 可以簡化成這樣：
```Swift

  var isExpanded:Bool = false
  var selectedRow = -1
 
  override func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
       
        
        if selectedRow == indexPath.row {
            isExpanded = !isExpanded
        } else {
            isExpanded = true
        }
        selectedRow = indexPath.row
        
        tableView.beginUpdates()
        tableView.endUpdates()
        
    }
    
    
    
    override func tableView(_ tableView: UITableView, heightForRowAt indexPath: IndexPath) -> CGFloat {
        
        if tableView.indexPathForSelectedRow?.row == indexPath.row && isExpanded {
            return expandHeight;
        }
        return normalHeight;  
    }
```

#### Reusable Cell repeating problems
[解法](https://fluffy.es/solve-duplicated-cells/)
- cell被reuse的時候，原本cell的設定，會跟著到reuse時又再出現。
- 解決方案是，在每個cell出現時，就先把原始設定再指定一次，然後再加入判斷值，做更動。


```Swift
func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
    let cell = tableView.dequeueReusableCell(withIdentifier: todoCellIdentifier, for: indexPath) as! TodoTableViewCell
        
    // reset (hide) the checkmark label
    cell.checkLabel.isHidden = true
    
    // get the Task object in the taskArray (data source)
    let task = self.taskArray[indexPath.row]
    
    // if the task has marked done, show the checkmark label
    if(task.done){
      cell.checkLabel.isHidden = false
    }
  
    cell.taskLabel.text = "Task \(indexPath.row)"
    return cell
}
```

#### TableView Reload
- 要在viewWillDispear這裹做reoload.(目前的心得）


#### TableView Scroll時，收起keyboard的做法
- viewDidLoad 加入 keyboardDismissMode = .onDrag
```Swift

        tableView.keyboardDismissMode = .onDrag

```
- scrollViewDidScroll 設定
```Swift
func scrollViewDidScroll(_ scrollView: UIScrollView) {
        if !tableView.isDecelerating {
                   view.endEditing(true)
               }
    }
    
```


#### TableView Scroll時，把navigation bar 收起來
```Swift
self.navigationController?.hidesBarsOnSwipe = true

```

#### Setup tableView in a UIView programmatically
```Swift
import UIKit

class AddTableView: UIView {
    
    
    var tableView = UITableView()
    
    
    override func draw(_ rect: CGRect) {
        self.addSubview(tableView)
        tableView.register(UITableViewCell.self, forCellReuseIdentifier: "cell")
        tableView.delegate = self
        tableView.dataSource = self
        setupTableViewConstraints()
        tableView.backgroundColor = .red
    }
    
    override func layoutSubviews() {
        //tableView.frame = self.bounds
    }
    
    func setupTableViewConstraints() {
        tableView.translatesAutoresizingMaskIntoConstraints = false
        NSLayoutConstraint.activate([
            tableView.topAnchor.constraint(equalTo: self.topAnchor),
            tableView.leadingAnchor.constraint(equalTo: self.leadingAnchor),
            tableView.trailingAnchor.constraint(equalTo: self.trailingAnchor),
            tableView.bottomAnchor.constraint(equalTo: self.bottomAnchor)
        ])
    }
}

extension AddTableView: UITableViewDelegate, UITableViewDataSource {
    
    //UITableViewDelegate
    func tableView(_ tableView: UITableView, didSelectRowAt indexPath: IndexPath) {
        print("you tap")
    }
    
    //UITableViewDataSource
    
    func tableView(_ tableView: UITableView, numberOfRowsInSection section: Int) -> Int {
        5
    }
    
    func tableView(_ tableView: UITableView, cellForRowAt indexPath: IndexPath) -> UITableViewCell {
        
        let cell  =  tableView.dequeueReusableCell(withIdentifier: "cell", for: indexPath)
        
        cell.textLabel?.text = "good"
        
        return cell
    }
    
```
#### reloadData, beginUdate等的差別
[source](https://jjeremy-xue.medium.com/swift-說說-tableview-reload-updates-110bded53c3c)
- reloadData 更新數據，刷新tableView（簡單且粗暴），重整整個表格的數據，並無動畫效果。

