# JS in Web

## 定義

#### 前端開發者在網頁上的操作方法，是經由瀏覽器這個執行平台，去操作JS的

## 瀏覽器上的JS包含

### JS

### BOM（瀏覽器物件模型）

{% hint style="info" %}
#### BOM：瀏覽器所有功能的核心，與網頁的內容無關
{% endhint %}

* 核心為 window物件 
* window提供的主要屬性為：`document`、`location`、`navigator`、`screen`、`history`、`frames` 
* windows扮演兩種角色：
  * 全域物件
  * JS用來與瀏覽器溝通的窗口：`alert`、`confirm` 
* 凡是在全域作用範圍內宣告的變數、物件、函式，都會自動變為全域物件屬性 
* 全域作用範圍無法使用 `delete`來移除

### DOM（文件物件模型）

* 將HTML以樹狀結構來表示的模型，稱DOM tree

### DOM vs BOM

* BOM：JS與瀏覽器溝通的窗口，跟內容無關 
* DOM：控制網頁的內容與節點

```javascript
// 得到tagName 為 xxx 的節點，並把他的文字內容改為 Hello World
document.getElementByTagName('xxx).textContext = "Hello World"
```

## 所謂的 &lt;script&gt; 放哪裡與怎麼取節點

* head 
  * 放在`<head>`中，有可能因為`<script>`要對DOM做事，而DOM還沒生成照成錯誤 
* body 
  * 可用 `docement.querySelector('#Hello')` 來找尋節點 
  * 父子節點 
    * 判斷是否有子節點：`hasChildNodes()` 
    * 取得第一個子節點：`firstChild()` 
    * 取得最後一個子節點：`lastChild()`。若無則`null` 
    * 取得兄弟節點：`parentNode()` 
  * 兄弟節點（若無下一個則回傳 `null`） 
    * 前一個兄弟節點：`previousSibling()` 
    * 下一個兄弟節點：`nextSibling()` 
  * 後面可接 
    * nodeName：就為節點名稱 
    * textContent：就為文字內容

## 遍歷 selector

* `document.gerElementById` &gt; 取得只會有一個節點，故沒有index / length屬性，節點受 js 程式影響

* `document.querySelector` &gt; 取得只會有一個節點，故沒有index / length屬性。節點不受 js程式影響。 
* `document.getElementsBy**` &gt; 取得集合，節點受 js程式影響 
* `document.querySelectorAll` &gt; 取得節點List，為靜態的，不受 js 程式刪除所影響

