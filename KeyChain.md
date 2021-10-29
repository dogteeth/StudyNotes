#### KeyChain
- [連結](https://www.appcoda.com.tw/app-security/)

- UserDefaults 只是將資料儲存為一個屬性列表檔案，存放於 App 的 Preferences 資料夾裡。它們並沒有以任何形式加密儲存在 App 中。基本上來說，藉由使用 Mac 的第三方程式像是 iMazing，即使手機沒有越獄 (Jailbreak)，你也可以輕易看到任何從 AppStore 下載的 App 內 UserDefaults 的資料。這些 Mac App 雖然只是設計來讓你瀏覽或管理你手機上的第三方程式檔案，但你也可以輕易地瀏覽任何 App 的 UserDefaults。

-在 iOS App 上儲存資料時你必須記住一點，UserDefaults 只是設計來儲存小量資料，像是使用者在 App 裡的偏好設定、或是一些完全不敏感的東西。要儲存 App 的敏感資料，我們應該使用 Apple 提供的 Security 服務。

![1*GSrgZbPEHGC_9Cy_lfDTPA](https://user-images.githubusercontent.com/18608853/139405726-01d25cc9-cb79-4ad3-b3bb-663482123cdf.png)

- CFString -> CF指的是 Core Foundation. ： Core Foundation框架是蘋果公司提供一套概念來源於Foundation框架，編程接口面向C語言風格的API。雖然在Swift中調用這種C語言風格的API比較麻煩，但是在OS X和iOS開發過程中，有時候使用CoreFoundation框架的API是非常方便的，例如在與C語言混合編碼的時候。Core Foundation框架與Foundation框架緊密相關，他們具有與相同的接口，但是不同。Core Foundation框架是基於C語言風格的，而Foundation框架是基於Objective-C語言風格的。在OS X和iOS程序代碼中經常會有多種語言風格的代碼混合在一起的情況，這使得我們開發變得更加麻煩。Core Foundation框架提供瞭一些不透明的數據類型，這些數據類型封裝瞭一些數據和操作，他們也可以稱為“類”，他們都繼承於CFType類，CFType是所用Core Foundation框架類型的根類。這些數據類型在Foundation框架中都有相應的數據類型與之對應，這些數據類型也有一些與Swift原生數據類型有對應關系。

#### C functions for KeyChains
Since the code hides items from ill-intentioned users, Keychain Services provide a set of C functions to interact with. Here are the APIs you’ll use to manipulate both generic and internet passwords:
- SecItemAdd(_:_:): Use this function to add one or more items to a keychain.
- SecItemCopyMatching(_:_:): This function returns one or more keychain items that match a search query. Additionally, it can copy - attributes of specific keychain items.
- SecItemUpdate(_:_:): This function allows you to modify items that match a search query.
- SecItemDelete(_:): This function removes items that match a search query.
