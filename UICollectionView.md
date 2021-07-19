#### 動作
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
