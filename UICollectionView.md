#### UICollectionViewCell 做自動寛度
```Swift

func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
    return CGSize(
    width: tabsArray[indexPath.row].size(withAttributes: [NSAttributedString.Key.font : UIFont.systemFont(ofSize: 17)]).width + 25,
    height: 32
    )
 }

```

#### UICollectionView Setup
- 設兩個delegate, UICollectionViewDataSource, UICollectionViewDelegate

- minimumLineSpacingForSectionAt：Asks the delegate for the spacing between successive rows or columns of a section. item cell之間的間隔設定。
- minimumInteritemSpacingForSectionAt： Asks the delegate for the spacing between successive items in the rows or columns of a section.



#### 設計UICollectionView
- 和UITableView一樣的概念
- 加入三個extension: UICollectionViewDataSource, UICollectionViewDelegate, UICollectionViewDelegateFlowLayout
- UICollectionViewDataSource: 處理 number of cells, dequeue the cell, 
- UICollectionViewDelegate: 處理 didselect the cell
- UICollectionViewDelegateFlowLayout: 處理 


- UICollectionViewDataSource
```Swift
extension ViewController: UICollectionViewDataSource {
    func collectionView(_ collectionView: UICollectionView, numberOfItemsInSection section: Int) -> Int {
        return 12
    }
    
    func collectionView(_ collectionView: UICollectionView, cellForItemAt indexPath: IndexPath) -> UICollectionViewCell {
        let cell = collectionView.dequeueReusableCell(withReuseIdentifier: MyCollectionViewCell.identifier, for: indexPath) as! MyCollectionViewCell
        
        cell.config(with: UIImage(named: "image")!)
        return cell
    }
}

```

- UICollectionViewDelegate
```Swift
extension ViewController: UICollectionViewDelegate {
    
    func collectionView(_ collectionView: UICollectionView, didSelectItemAt indexPath: IndexPath) {
        collectionView.deselectItem(at: indexPath, animated: true)
        print("good tap!")
    }
}

```

- UICollectionViewDelegateFlowLayout

```Swift
extension ViewController: UICollectionViewDelegateFlowLayout {
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, sizeForItemAt indexPath: IndexPath) -> CGSize {
        
        let size:CGFloat = view.bounds.width/3 - 3
        return CGSize(width: size, height: size)
    }
    
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, minimumInteritemSpacingForSectionAt section: Int) -> CGFloat {
        return 1
    }
    
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, minimumLineSpacingForSectionAt section: Int) -> CGFloat {
        return 1
    }
    
    func collectionView(_ collectionView: UICollectionView, layout collectionViewLayout: UICollectionViewLayout, insetForSectionAt section: Int) -> UIEdgeInsets {
        return UIEdgeInsets(top: 1, left: 2, bottom: 1, right: 2)
    }
}
```

- viewDidLoad

```swift
        collectionView.collectionViewLayout = UICollectionViewFlowLayout()
        collectionView.delegate = self
        collectionView.dataSource = self
```

- Scroll Direction Setup
```Swift
       if let layout = collectionView.collectionViewLayout as? UICollectionViewFlowLayout {
            layout.scrollDirection = .horizontal
            }
```
- set to the target cell
```Swift
let indexPath = IndexPath(item: 2, section: 0)
self.collectionView.scrollToItem(at: indexPath, at: [.centeredVertically, .centeredHorizontally], animated: true)
```


#### 自動收放的 collectionView height

- 先做UIView的動畫extension
```Swift
extension UIView {
    
    func setView(view: UIView, hidden: Bool) {
        UIView.transition(with: view, duration: 0.05, options: .curveEaseInOut, animations: {
            view.isHidden = hidden
        })
    }
}
```

- BTN的部份再加入判斷，


```Swift
@IBAction func viewOpenAndClose(_ sender: UIButton) {
        
        viewIsOpen = !viewIsOpen
        
        if viewIsOpen == true {
            collectionView.setView(view: collectionView, hidden: false)
            openAndCloseBTN.setImage(UIImage(systemName: "chevron.down"), for: .normal)
        } else  {
            collectionView.setView(view: collectionView, hidden: true)
            openAndCloseBTN.setImage(UIImage(systemName: "chevron.up"), for: .normal)
        }
        
    }


```
 *** 要讓layouts自動調整，放進同一個stack就可以有這樣的功能了。


#### 讓 Cell有圓角 
```Swift
extension UICollectionViewCell {
    func shadowDecorate() {
        let radius: CGFloat = 10
        contentView.layer.cornerRadius = radius
        contentView.layer.borderWidth = 1
        contentView.layer.borderColor = UIColor.clear.cgColor
        contentView.layer.masksToBounds = true
    
        layer.shadowColor = UIColor.black.cgColor
        layer.shadowOffset = CGSize(width: 0, height: 1.0)
        layer.shadowRadius = 2.0
        layer.shadowOpacity = 0.5
        layer.masksToBounds = false
        layer.shadowPath = UIBezierPath(roundedRect: bounds, cornerRadius: radius).cgPath
        layer.cornerRadius = radius
    }
}
```

#### 讓 collectionView reload時有個動畫的感覺
```Swift

self.collectionView.performBatchUpdates({
                            let indexSet = IndexSet(integersIn: 0...0)
                            self.collectionView.reloadSections(indexSet)
                        }, completion: nil)
        let indexPath = IndexPath(item: 0, section: 0)
                    self.collectionView.scrollToItem(at: indexPath, at: [.centeredVertically, .centeredHorizontally], animated: true)
        
```

#### 讓 collectionView cell 有 longPress的功能
*note: view controller要設extension: UIGestureRecognizerDelegate
```Swift
private func setupLongGestureRecognizerOnCollection() {
        let longPressedGesture = UILongPressGestureRecognizer(target: self, action: #selector(handleLongPress(gestureRecognizer:)))
        longPressedGesture.minimumPressDuration = 0.5
        longPressedGesture.delegate = self
        longPressedGesture.delaysTouchesBegan = true
        collectionView?.addGestureRecognizer(longPressedGesture)
    }

    @objc func handleLongPress(gestureRecognizer: UILongPressGestureRecognizer) {
        if (gestureRecognizer.state != .began) {
            return
        }

        let p = gestureRecognizer.location(in: collectionView)

        if let indexPath = collectionView?.indexPathForItem(at: p) {
            centerCaseLocation(caseItem: caseNearBy10Kilo[indexPath.row])
            print("Long press at item: \(indexPath.row)")
        }
    }

```

#### UICollectionView，系統設定cell selected.
```Swift
collectionView.selectItem(at: NSIndexPath(item: 0, section: 0) as IndexPath, animated: false, scrollPosition: .centeredHorizontally)
```
- 加入上面的程式
- 加的地方，選擇放在viewDidAppear, view load完，同時也appear後，帶出這個程式。
- 若其它內容也需要出現的資料，也一起在view load完後。就會在頁面出現的時候，一起load出來。
```Swift
override func viewDidAppear(_ animated: Bool) {
        collectionView.selectItem(at: NSIndexPath(item: 0, section: 0) as IndexPath, animated: false, scrollPosition: .centeredHorizontally)
        contentArray = dummyListArrayOne
        tableView.reloadData()
    }

```
