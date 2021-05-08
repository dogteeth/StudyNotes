#### Prepare for segue 什麼時候被呼叫？
When a segue is triggered – perhaps through a button press or a table view selection – the prepare(for:) method will be called on your view controller, at which point you can configure your destination view controller by setting some properties.


#### segue有四種
- show : 以全營幕的方式程現。（支援導覽列控制器）
- show detail ： 如果視圖是分割成左右兩半，會出現在右方的視圖。若視圖非分割狀態，則會以全營幕出現。（不支援導覽列控制器）
- present modally：可設成全營幕，也可以是個矩型在中間。或是由下往上滑動。
- present as popover：在大營幕是pop up小視窗。在小營幕則是全營幕。


#### strong, weak 與 unowned
[資料來源](https://www.appcoda.com.tw/memory-management-swift/)

- 與 Swift 記憶體管理的 Automatic Reference Counting （自動參考計數機制, ARC）有關。
- Reference Counting 是以一項技術，是將資源（例如物件、記憶體或磁盤空間等）被參考的次數保存起來。簡單來說，ARC 可以把參考儲存到記憶體中，並自動清除沒有在使用的參考。
- Reference Counting 僅適用於類別 (class) 的實例 (instance)，而不適用於結構 (structures) 和枚舉 (enumerations)，因為他們兩個都是數值型別 (Value Type)，而不是參考型別 (Reference Type)。
- Swift 的記憶體管理會一直運作，你不需要自己去考慮記憶體管理的問題。當實例不再被使用時，ARC 會自動釋放所佔用的記憶體。
- 每當你要初始化 init() 一個類別時，ARC 會自動配置記憶體來儲存資料；更具體來說，就是一部份的記憶體配置了給實例，並同時在屬性配置了數值，所以當不再需要實例時，deinit() 就會被呼叫，而 ARC 會將此實例的記憶體空間釋出。
- ![arc-strong-weak-unowned](https://user-images.githubusercontent.com/18608853/117527448-bd744600-affe-11eb-870c-713f5b7c141d.png)


