# THINK-3

THINK篇主要述說在寫Vue時的基本觀念

而大部分的資料都可以從官網獲得：

* [掘金](https://juejin.im/post/5d59f2a451882549be53b170) 
* [Vue 官網 - 教程](https://cn.vuejs.org/v2/guide/)

## 21.TALK SSR

#### SSR優點

* 更好的SEO：因為SPA的頁面內容是通過 Ajax 獲取，而搜尋引擎不會等待Ajax 異步完成後再抓取頁面內容，所以在SPA 中抓取不到頁面通過Ajax 獲取的內容。而SSR是服務端已經渲染好的畫面，所以搜尋引擎可以抓取渲染好的資料。 
* 更快加載畫面：SSR直接由服務端渲染好頁面而直接返回顯示，無需等待下載js文件再去渲染，所以SSR有更快的加載速度。

#### SSR缺點

* 更多的開發條件限制：因為服務器選染只支持 BeforeCreate & Created 兩個鉤子函數，會導致一些擴展庫需要特殊處理，才能在服務端渲染應用程序中執行。 
* 更多的服務端負載：在 Node.js 中渲染完整的應用程序，顯然會比僅僅提供靜態文件的 server 更佔用大量的CPU。

## 22.Vue-router

#### Vue-router 共有三種路由模式：hash、history、abstract。

```javascript
switch (mode) {
  case 'history':
	this.history = new HTML5History(this, options.base)
	break
  case 'hash':
	this.history = new HashHistory(this, options.base, this.fallback)
	break
  case 'abstract':
	this.history = new AbstractHistory(this, options.base)
	break
  default:
	if (process.env.NODE_ENV !== 'production') {
	  assert(false, `invalid mode: ${mode}`)
	}
}
```

* `hash`：使用 URL hash 來做路由。支持所有瀏覽器。 
  * 將 `location.hash` 的值設定為 URL 中 \# 後面的內容 
  * 特性： 
    * 為客戶端的一種狀態，當向服務器端發出請求時，hash 部分不會被發送。 
    * hash改變，會變成歷史紀錄。 
    * 可以通過 `a tag` 設置 `href` 屬性，當用戶點擊時，此URL 的 `hash` 值會改變。 
    * 可以使用 `hashchange` 來監聽 hash 的變化，藉此對頁面進行跳轉。 
* `history`：依賴HTML5 History API 和伺服器配置。 
  * 實現原理：利用`history.pushState()`_**（新增一個歷史紀錄）**_ & `history.replaceState()`_**（替換當前的歷史紀錄）**_。這兩個API可以在不進行刷新的情況下，操作瀏覽器的歷史紀錄。 
  * 特性： 
    * `pushState`、`replaceState`：操作實現URL的變化。 
    * 可使用`popstate` 來監聽 url 的變化，從而對頁面進行跳轉。 
    * `history.pushState` & `history.replaceState` 不會觸發 `popstate`，我們需要透過手動觸發頁面跳轉。 
* `abstract`：支持所有 JS 運行環境，如果Node.js 端沒發現瀏覽器的 API，路由會自動進入這個模式。

## 23.MVVM

#### Basic

* 源自經典的MVC模式，MVVM促進了前後端分離，提高了前端開發效率。MVVM 核心為 VM（ViemModel）層，像一個中繼站，負責轉換Model 中的數據對象來讓數據變得更加容易管理和使用。 
* VM 向上與視圖層進行雙向數據綁定，向下與Model 層通過接口請求進行數據交互，達呈上啟下作用。 
* 名詞分析： 
  * V：為視圖層，為用戶介面。前端由HTML 和 CSS 來建構。 
  * M：數據模型，泛指後端進行的各種業務邏輯處理和數據操控，對於前端來說是後端API接口。 
  * VM：在這裏，前端開發者對從後端獲取的數據進行轉換處理，做二次封裝，以生成符合View層使用預期的視圖數據模型。 
    * Notice：封裝出來的數據包含視圖的狀態和行為兩部分，而Model只包含狀態 

#### 附上作者的Code 讓大家參考了解

* _**View**_

```javascript
<div id="app">
    <p>{{message}}</p>
    <button v-on:click="showMessage()">Click me</button>
</div>
```

* _**ViewModel**_

```javascript
var app = new Vue({
    el: '#app',
    data: {  // 描述視圖狀態
        message: 'Hello Vue!', 
    },
    methods: {  // 描述視圖行為  
        showMessage(){
            let vm = this;
            alert(vm.message);
        }
    },
    created(){
        let vm = this;
        // Ajax 獲取 Model 數據
        ajax({
            url: '/your/server/data/api',
            success(res){
                vm.message = res;
            }
        });
    }
})
```

* _**Model**_

```javascript
{
    "url": "/your/server/data/api",
    "res": {
        "success": true,
        "name": "IoveC",
        "domain": "www.cnblogs.com"
    }
}
```



















