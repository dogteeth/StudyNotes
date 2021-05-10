#### [資料來源](https://ithelp.ithome.com.tw/articles/10196319)
#### [wikiAPI說明文件](https://www.mediawiki.org/wiki/API:Main_page)

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

***

[Wiki文件筆記](https://www.mediawiki.org/wiki/API:Main_page)

- The maxlag parameter: If your task is not interactive, i.e. a user is not waiting for the result, you should use the maxlag parameter. The value of the maxlag parameter should be an integer number of seconds. This will prevent your task from running when the load on the servers is high. Higher values mean more aggressive behavior, lower values are nicer. Exmaple: maxlag=1
- All new API users should use JSON.
- Get a content of a page，有三個方法，1）Revisions API (as wikitext)，2） Parse API (as HTML or wikitext)，3）API of the TextExtracts extension.
- 成
- Get a content of a page，有三個方法，1）Revisions API (as wikitext)，2） Parse API (as HTML or wikitext)，3）API of the TextExtracts extension.


#### 測試連結

- 取得taiwan這個名字的相關圖片。
https://en.wikipedia.org/w/api.php?action=query&titles=taiwan&format=json&prop=images&format=json

- get the image link, by the title of the image.
https://en.wikipedia.org/w/api.php?action=query&titles=File:Test.jpg&prop=imageinfo&iilimit=50&iiend=2007-12-31T23:59:59Z&iiprop=timestamp|user|url

- 搜尋有關taiwan的網頁，並回傳一頁的wiki 
https://en.wikipedia.org/w/api.php?action=query&list=search&srsearch=taiwan&srlimit=1&&format=json

- 取得pageid後的短網址
http://en.wikipedia.org/?curid=18630637

- 取得link
https://en.wikipedia.org/w/api.php?action=query&format=json&prop=info&generator=allpages&inprop=url&gapfrom=Apple&gaplimit=5

- api endpoints
https://nl.wikipedia.org/w/api.php  Dutch Wikipedia API

- 直接用網頁開始wiki search 結果
https://zh.wikipedia.org/w/index.php?search=QUERY&title=taiwan&fulltext=Search



#### [youtuber的實作](https://www.youtube.com/watch?v=Dk6Wopar10k&t=129s)
1:20:37左右，說明api的使用方式

```swift

?action=query
&generator=search //generator search的方式,可以讓我一次做多種search的要求,在此例做的是，pageimages, extracts的search
	&gsrsearch=yoursearchtext //我要置入search的值
	&gsrlimit=20 //最多給20個條目（沒有token最多只能要20個）
&prop=pageimages|extracts //給我兩個東西，pageimages, extracts
	&exchars=130 //給我130個文字。
	&exintro //要多個extracts這個一定要放。
	&explaintext //給我文字。
	&exlimit=max //給我20個條目。
&format=json
&origin=*

```


https://www.mediawiki.org/wiki/API:Query

action=query

prop:
- extracts: Returns plain-text or limited HTML extracts of the given pages.
- info: Get basic page information.
- images: Returns all files contained on the given pages.
- iwlinks: Returns all interlanguage links from the given pages.
- pageviews: Shows per-page pageview data (the number of daily pageviews for each of the last pvipdays days).

list:
- allimages: Enumerate all images sequentially.
- alllinks: Enumerate all links that point to a given namespace.
- allpages: Enumerate all pages sequentially in a given namespace.
- random: Get a set of random pages.
- search: Perform a full text search.

indexpageids: Include an additional pageids section listing all returned page IDs.

titles: A list of titles to work on. Separate values with | or alternative.Maximum number of values is 50 (500 for clients allowed higher limits).

pageids: A list of page IDs to work on. Type: list of integers. Separate values with | or alternative. Maximum number of values is 50 (500 for clients allowed higher limits).

generator: Get the list of pages to work on by executing the specified query module. Note: Generator parameter names must be prefixed with a "g".
- links: Returns all links from the given pages.
- images: Returns all files contained on the given pages.
- random: Get a set of random pages.

取得圖片：
- prop=pageimages
- prop=pageimages|pageterms, to get image and description.
- piprop=original, get the orignial 
- piprop=thumbnail&pithumbsize=600format=json&formatversion=2


