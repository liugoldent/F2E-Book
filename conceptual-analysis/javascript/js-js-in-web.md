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

