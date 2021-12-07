```Swift
let alert = UIAlertController(title: "Delete Player", message: nil , preferredStyle: .alert)
        
        alert.addAction(UIAlertAction(title: "cancel", style: .cancel, handler: nil ))
        alert.addAction(UIAlertAction(title: "confirm", style: .default, handler: nil))
        present(alert, animated: true, completion: nil)

```
