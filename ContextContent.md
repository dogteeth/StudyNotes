##### BarButton加入ContextContent

- 設計 menuActionList, menuList兩個變數

```Swift
    var menuAction : [UIAction] {
        return [
            UIAction(
                title: "Action-One",
                image: UIImage(systemName: "person"),
                handler: { _ in
                    print("action one pressed")
                }),
            UIAction(
                title: "Action-Two",
                image: UIImage(systemName: "eyes"),
                handler: { _ in
                    print("action two pressed")
                })
        
        ]
    }
    
    var menuList : [UIMenu] {
        return [
            UIMenu(title: "1",
                   image: nil,
                   identifier: nil,
                   options: [],
                   children: []),
            UIMenu(title: "2",
                   image: nil,
                   identifier: nil,
                   options: [],
                   children: [])
        ]
    }

```
- 在viewDidLoad裹，將bar button的 IBOulet以 menu的method，加入 menuAction, menuList
- children: [ ] 放的是UIMenuElement。UIElement : An object representing a menu, action, or command.所以也可以直接放入ActionList, 或是兩層次，先用List，再放Action。
- 重要：如果只有一個層次，一定是Action. 只放List不會有反應。

```Swift
barButton.menu = UIMenu(
            title: String,
            image: UIImage?,
            identifier: UIMenu.Identifier?,
            options: UIMenu.Options,
            children: [UIMenuElement])
```

#### Reading Material [The Comprehensive Guide to iOS Context Menus](https://kylebashour.com/posts/context-menu-guide)


#### imageView 加入 ContextContent
- imageView(UIImageView的IBOutlet)，需要設 .isUserInteractionEnabled = true
- UIContextMenuInteraction 設 delegate

```Swift
override func viewDidLoad() {
        super.viewDidLoad()
        
        imageView.isUserInteractionEnabled = true
        let interaction = UIContextMenuInteraction(delegate: self)
        imageView.addInteraction(interaction)
}
```
- 做extension UIContextMenuInteractionDelegate
- 在這個Delegate裹，只有一個function要做: configurationForMenuAtLocation。它需要回傳UIContextMenuConfiguration。

```Swift
extension ItemDetailTVC : UIContextMenuInteractionDelegate {
    func contextMenuInteraction(_ interaction: UIContextMenuInteraction, configurationForMenuAtLocation location: CGPoint) -> UIContextMenuConfiguration? {

        UIContextMenuConfiguration(identifier: nil, previewProvider: nil) { _ in
            let menuCheckInAction = UIAction(title: "到訪打卡", image: UIImage(systemName: "pin")) { _ in
                print("打卡押了")
            }
            let menuBookMarkAction = UIAction(title: "加入書籤", image: UIImage(systemName: "bookmark")) { _ in
                print("書籤押了")
            }
            return UIMenu(title: "", children: [menuBookMarkAction, menuCheckInAction])

        }
    }
}
```
