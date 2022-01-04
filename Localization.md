#### [iOS 關於多國語系的那些事](https://franksios.medium.com/ios-localization-本地化-7b16b58bb9df)

#### 三個主要檔案
- 元件所有顯示的多國語系文字(Localizable.strings)
- App的名稱和Info.plist𥚃多國語系的描述(InfoPlist.strings)
- 圖片的多國語系

#### 作業方式
- 在 Project > Info > Localization，加入要支援的語系（如德文，日文...)
- 新增 Strings File, 命名為 "Localizable", 它的檔案全名會是"Localizable.strings".
- "Localizable.strings" 的 editory裹，將要支援的語文全打勾。打勾的同時，就新增出相對應的file頁面
- 在每一個語言的頁面裹加入文字對照表即完成。
- code: label.text = NSLocalizedString("XXXXX", comment:"")

#### 取得APP現有語言設定
```Swift
let langCode = Bundle.main.preferredLocalizations[0]
let usLocale = Locale(identifier: "en-US")
var langName = ""
if let languageName = usLocale.localizedString(forLanguageCode: langCode) {
    langName = languageName
}
```
- Use Bundle.main.preferredLocalizations[0] to get the language your app's UI is currently displayed in. Don't use Locale.current because it describes the region format (time, currency, distance, etc) and has nothing to do with language.
- Locale.current returns the current locale, that is, the value set by Settings > General > Language & Region > Region Formats. It has nothing to do with the language that your app is running in. It's perfectly reasonable, and in fact quite common, for users in the field to have their locale and language set to 'conflicting' values. For example, a native English speaker living in France would have the language set to English but might choose to set the locale to French (so they get metric weights and measures, 24 time, and so on).
- The language that your app runs in is determined by the language setting, that is, Settings > General > Language & Region > Preferred Language Order. When the system runs your app it takes this list of languages (the preferred list) and matches it against the list of languages that your app is localised into (the app list). The first language in the preferred list that exists in the app list is the language chosen for the app. This is what you'll find in the first entry of the main bundle's preferredLocalizations array.
