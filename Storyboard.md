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
view.addSubview(secondView.view)
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


#### 手動加入Sidebar
- mainView
```Swift
import UIKit

class ViewController: UIViewController {
    
    let secondView = SecondView()
    var sideBarIsOpen = false
    override func viewDidLoad() {
        super.viewDidLoad()
        
        navigationItem.title = "Main View"
        
        addChild(secondView)
        view.addSubview(secondView.view)
        setSeconViewConstraints()
        
        secondView.didMove(toParent: self)
        
    }
    
    func setSeconViewConstraints() {
        
        
        secondView.view.translatesAutoresizingMaskIntoConstraints = false
        secondView.view.topAnchor.constraint(equalTo: view.safeAreaLayoutGuide.topAnchor).isActive = true
        secondView.view.bottomAnchor.constraint(equalTo: view.safeAreaLayoutGuide.bottomAnchor).isActive = true
        secondView.view.leadingAnchor.constraint(equalTo: view.safeAreaLayoutGuide.trailingAnchor, constant: 0).isActive = true
        secondView.view.widthAnchor.constraint(equalToConstant: 100).isActive = true
        
    }
    
    
    
    @IBAction func sidebarBTN(_ sender: UIBarButtonItem) {
        sideBarIsOpen = !sideBarIsOpen

        if sideBarIsOpen == true {
            UIView.animate(withDuration: 0.1) {
                self.secondView.view.frame.origin.x -= 100                
            }
        } else {
            UIView.animate(withDuration: 0.1) {
                self.secondView.view.frame.origin.x += 100
                self.view.backgroundColor = .white

            }
        }
       
        print("press sidbarBTN")
    
    }
}


```
- secondView
```Swift
import UIKit

class SecondView: UIViewController {

    override func viewDidLoad() {
        super.viewDidLoad()

        view.backgroundColor = .cyan
    }
    

}
```
