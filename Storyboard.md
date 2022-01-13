#### No Storyboard Setup
- 1. remove files: delete SceneDelegate, Main, two files.
- use shift+command+F, call out general search, search for "main"
- 2. update info.plist: 
        - 1.) delete INFOPLIST_KEY_UIMainStroyboardFile = Main, 
        -  <img width="1139" alt="deleteMain" src="https://user-images.githubusercontent.com/18608853/149269883-8c43bba3-c906-4f91-9491-1efac5c5704c.png">

        
        
        - 2) go to Info.plist Bankery Main -> Application Scene Mainfest, delete this thread.
- 3. udpate AppDelegate: Delete anything in AppDelegate.

####
- viewDidLoad: 只會在 App 加載時被呼叫一次
- viewDidAppear: 在於每次進入畫面時 viewDidAppear 就會被呼叫
- viewDidLayoutSubviews: 

Apple gave a very good explanation on this by saying that it is called to notify the view controller that its view has just laid out its subviews. In another word, viewDidLayoutSubviews is called every time the view is updated, rotated or changed or it’s bounds change. The keyword here is bounds change.
        
But know that with viewDidLayoutSubviews, it only take places after all the auto layout or auto resizing calculations on the views have been applied. Meaning the method viewDidLayoutSubviews is called every time the view size changes and the view layout has been recalculated.

Every time you build an app, viewDidLayoutSubviews will take place right after viewDidLoad because remember that viewDidLayoutSubviews take place when the layout calculation is applied. Then, when you rotate your app, viewDidLayoutSubviews will take place again and this only work from portrait to landscape and landscape back to portrait. And not from landscape left to landscape right. 


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
