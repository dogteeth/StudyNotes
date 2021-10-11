#### 將一個storyboard加到一個畫面裹。
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
