#### Prepare for segue 什麼時候被呼叫？
When a segue is triggered – perhaps through a button press or a table view selection – the prepare(for:) method will be called on your view controller, at which point you can configure your destination view controller by setting some properties.


#### segue有四種
- show : 以全營幕的方式程現。（支援導覽列控制器）
- show detail ： 如果視圖是分割成左右兩半，會出現在右方的視圖。若視圖非分割狀態，則會以全營幕出現。（不支援導覽列控制器）
- present modally：可設成全營幕，也可以是個矩型在中間。或是由下往上滑動。
- present as popover：在大營幕是pop up小視窗。在小營幕則是全營幕。


#### strong, weak 與 unowned
