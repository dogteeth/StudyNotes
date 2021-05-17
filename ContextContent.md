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
