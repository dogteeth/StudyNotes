[Reusable Image Cache in Swift](https://medium.com/flawless-app-stories/reusable-image-cache-in-swift-9b90eb338e8d)


- Using NSCache as a storage
- Memory FootPrint
  - pages of memory
  - typically 16 kb in size
  - numbers of pages  X page size = Memory in Use
  - 50 kb的 image, = 3 pages and less than 1 page.
 
An app has three kinds of memory
- clean: 
- dirty: app 寫進去的所有資料都算 dirty
- compressed: compressed the pages not in use, and decompressed when in use.


當 App 進入背景或重新啟動時，圖片將需要重新抓取。因為當 App 進入背景時，NSCache 裡的內容會被移除。 而當 App 重新啟動時， NSCache 也會重新產生，不會有之前儲存的資料。
