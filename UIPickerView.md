- UIPickerView就像UITableView一樣的概念
- 需要 delegate, datasource的設定。

#### 設定UIPickerView的方式
- VC需要extension: UIPickerViewDelegate, UIPickerViewDataSource
- 建立 pickerView的IBOutlet
- delegate, datasource都要設 delegate = self
- picker內的文字，製作array。
- 增加protocol, protocol相關function如下：

```Swift
func numberOfComponents(in pickerView: UIPickerView) -> Int {
        return 1
    }
    
    func pickerView(_ pickerView: UIPickerView, numberOfRowsInComponent component: Int) -> Int {
        return pickerData.count
    }
    
    func pickerView(_ pickerView: UIPickerView, titleForRow row: Int, forComponent component: Int) -> String? {
        return pickerData[row]
    }
    
    func pickerView(_ pickerView: UIPickerView, didSelectRow row: Int, inComponent component: Int) {
        print("you select\(row)")
    }
```

[Picker Example Study](https://makeapppie.com/2014/10/21/swift-swift-formatting-a-uipickerview/)


- 改變pickerView內的文字大小
```Swift
func pickerView(_ pickerView: UIPickerView, viewForRow row: Int, forComponent component: Int, reusing view: UIView?) -> UIView {
        var pickerLabel: UILabel? = (view as? UILabel)
        if pickerLabel == nil {
            pickerLabel = UILabel()
            pickerLabel?.font = UIFont(name: "Arial", size: 16)
            pickerLabel?.textAlignment = .center
        }
        pickerLabel?.text = pickerData[row]
        pickerLabel?.textColor = UIColor.label

        return pickerLabel!
    }
```

#### UIPickerView上下選項的漸層
- pickerView的height會決定上下選項漸層的出現範圍。
- 若要上下選項不要出現，則把height縮小到只出現現有的Picker即可。
