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

