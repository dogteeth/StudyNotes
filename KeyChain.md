#### KeyChain與UserDefautls
- UserDefaults 只是將資料儲存為一個屬性列表檔案，存放於 App 的 Preferences 資料夾裡。它們並沒有以任何形式加密儲存在 App 中。基本上來說，藉由使用 Mac 的第三方程式像是 iMazing，即使手機沒有越獄 (Jailbreak)，你也可以輕易看到任何從 AppStore 下載的 App 內 UserDefaults 的資料。這些 Mac App 雖然只是設計來讓你瀏覽或管理你手機上的第三方程式檔案，但你也可以輕易地瀏覽任何 App 的 UserDefaults。

-在 iOS App 上儲存資料時你必須記住一點，UserDefaults 只是設計來儲存小量資料，像是使用者在 App 裡的偏好設定、或是一些完全不敏感的東西。要儲存 App 的敏感資料，我們應該使用 Apple 提供的 Security 服務。

![1*GSrgZbPEHGC_9Cy_lfDTPA](https://user-images.githubusercontent.com/18608853/139405584-6a911f47-bb85-4d38-9139-490ec092e157.png

