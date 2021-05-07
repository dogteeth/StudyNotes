#### [資料來源](https://ithelp.ithome.com.tw/articles/10196319)

##### Basic
- Basic URL : https://en.wikipedia.org/w/api.php
- 可使用Wiki提供的Sandbox進行request的測試： https://www.mediawiki.org/wiki/Special:ApiSandbox

##### 重要參數
- action
  * action=query
    * titles：設定要查詢維基頁面的title, 如：titles=New%20York，(需要URL Encoded)。
    * prop：回傳頁面哪些attributes, 如：
      * extracts 會回傳特定頁面上的文字或 HTML，可以加上 exlimit 設定回傳幾個 extract、exchars 設定 extract的長短。
      * categories：回傳頁面的分類
      * images：回傳頁面上的附加圖片檔
      * 更多的設定，參考文件說明
    * list：指名抓取特定 list 結果
  * action=parse：把內容傳入以得到想要的結果，比方說利用指定 titles 、pageId、page 的方法抓取頁面然後加上 prop=wikitext 來把內容改成wikitext 的格式。
  * action=opensearch：可以獲得特定關鍵字的簡短介紹，加上以下參數
    * namespace：頁面的種類，預設是 0，也就是主條目
    * （必選）搜尋關鍵字
    * format：預設是 json
    * limit：回傳結果數量  
- format
  * format回傳的資料有多種json, xml, php, jsonfm.
  * 預設是jsonfm（此格式是網頁型態）
  * 建議：format=json
- origin
  * 對於需要認証的request，在這裹需要放入你的網站網址。
  * 不需要認証的request，直接以星號處理即可：origin=*


#### Networking概念
- 跨來源資源共用標準的運作方式：藉由加入新的 HTTP 標頭讓伺服器能夠描述來源資訊以提供予瀏覽器讀取。另外，針對會造成副作用的 HTTP 請求方法（特別是 GET 以外的 HTTP 方法，或搭配某些 MIME types 的 POST 方法），規範要求瀏覽器必須要請求傳送「預檢（preflight）」請求，以 HTTP 的 OPTIONS (en-US) 方法之請求從伺服器取得其支援的方法。當伺服器許可後，再傳送 HTTP 請求方法送出實際的請求。伺服器也可以通知客戶端是否要連同安全性資料（包括 Cookies 和 HTTP 認證（Authentication）資料）一併隨請求送出。
