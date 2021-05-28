#### Segment的使用
- segment index 來做判斷後續的動作。

```Swift

 @IBAction func readingOrVisitingChooseBTN(_ sender: UISegmentedControl) {

        if sender.selectedSegmentIndex == 0 {
            
            //tableView selected
            mapView.isHidden = true
            tableView.isHidden = false
        }else {
            
            //mapView selected
            mapView.isHidden = false
            tableView.isHidden = true
            refreshMapAnnotations()
        }
    }
```
