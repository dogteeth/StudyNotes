#### 三個主要檔案
[iOS 關於多國語系的那些事](https://franksios.medium.com/ios-localization-本地化-7b16b58bb9df)
- 元件所有顯示的多國語系文字(Localizable.strings)
- App的名稱和Info.plist𥚃多國語系的描述(InfoPlist.strings)
- 圖片的多國語系

#### 作業方式
- 在 Project > Info > Localization，加入要支援的語系（如德文，日文...)
- 新增 Strings File, 命名為 "Localizable", 它的檔案全名會是"Localizable.strings".
- "Localizable.strings" 的 editory裹，將要支援的語文全打勾。打勾的同時，就新增出相對應的file頁面
- 在每一個語言的頁面裹加入文字對照表即完成。
- code: label.text = NSLocalizedString("XXXXX", comment:"")

