#### add storyboard to a view 
```Swift
isOpen = !isOpen
        if isOpen == true {
            guard let myVC = self.storyboard?.instantiateViewController(withIdentifier: "SidebarVC") else { return }
            let navController = UINavigationController(rootViewController: myVC)

            self.navigationController?.present(navController, animated: true, completion: nil)
        } else {
            self.dismiss(animated: true, completion: nil)

        }****
```


#### add storyboard to a view 

```Swift
         
addChild(sidbarVC)
setSidebarConstraints()
sidbarVC.didMove(toParent: self)

```
#### remove storyboard to a view 

```Swift
         
willMove(toParent: nil)
sidbarVC.view.removeFromSuperview()
//以下這一句，一旦它被移走，就不可能再出現, unless you initiate the view again.
removeFromParent()
```
