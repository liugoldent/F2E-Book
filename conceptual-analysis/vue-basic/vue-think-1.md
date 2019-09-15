# THINK-1

THINK篇主要述說在寫Vue時的基本觀念

而大部分的資料都可以從官網獲得：

* [掘金](https://juejin.im/post/5d59f2a451882549be53b170) 
* [Vue 官網 - 教程](https://cn.vuejs.org/v2/guide/)

## 0.鉤子：

* 具有既定生命週期的框架，在生命週期各個階段留給用戶執行的一些_**特定操作函數**_。

## 1.為何使用V-for 時，必須加上Key值？

參考資料：[CSDN-「Vue v-for 中的key」](https://blog.csdn.net/qq_35285627/article/details/81012902)

```text
<div v-for="item in items" :key="item.id">
```

Ans：  
為了給Vue一個提示，方便它能追蹤每個節點的身份。並且理想的`Key`是唯一的值。  
並且為了避免錯誤的渲染。

## 2.Vue 傳遞資料的方式

參考資料：[VueJS-元件-Component-之間資料傳遞的方式](https://kuro.tw/posts/2018/08/22/VueJS-%E5%85%83%E4%BB%B6-Component-%E4%B9%8B%E9%96%93%E8%B3%87%E6%96%99%E5%82%B3%E9%81%9E%E7%9A%84%E6%96%B9%E5%BC%8F/)

Ans：

* `Data` 
* 父給子：`Props` / 子給父：`$emit`   
  * vue 組件的基礎。 
* `ref` & `$parent`  /  `$children` 
  * `ref`：如果用於DOM上，就是指向 DOM。如果用於子組件，就是指向組件實例。 
  * `$parent` / `$children`：訪問父/子實例 
* `EventBus（$emit / $on）`：適用於父子、隔代、兄弟組件通信 
  * 此種方法，透過一個 Vue 實例作為中央事件總線（事件中心），用它來觸發事件和監聽事件，從而實現任何組件間的通信，包括父子、隔代、兄弟組建。 
* `$attrs / $listeners`：用於隔代組件通信 
  * `$attrs`：包含了父作用域不被`prop`所識別的特性綁定。當一個組建沒有聲明任何 `prop` 時，這裡會包含所有父作用域的綁定（class & style 除外），並且可以通過 v-bind="$attrs"傳入內部組件。通常配合`inheritAttrs`。 
  * `$listeners`：包含父作用域中的 `v-on` 事件監聽器。可以通過 `v-on="$listeners"` 傳入內部組件。 
* `provide / inject`：適用於隔代組件通信 
  * 祖先組件通過 `provider` 來提供變量，然後在子組件中通過 `inject` 來注入變量。有點主動提供與依賴注入的關係。 
* Vuex：適用於父子、隔代、兄弟組件通信。 
  * Vuex 為狀態管理模式。 
  * 每一個 Vuex應用的核心是 `store`。”`store`“ 基本上是一個容器 包含著我們大部分使用的狀態（`state`） 
  * 當Vue 組件從 store 中讀取狀態時，若 _**store 狀態發生改變**_，相應的_**組件**_也會相應地得到_**更新**_。 
  * 改變 store 的唯一途徑 就是 _**提交（commit）mutation**_。這樣使得我們可以方便地跟蹤每一個狀態的變化。 
  * 動作過程：_**commit mutation**_ -&gt; _**store 狀態改變**_ -&gt; _**組件更新**_。



## 3.Vue 生命週期

參考資料：[Vue生命週期函數](https://blog.csdn.net/chen1042246612/article/details/89190217)

Ans：

* BeforeCreate：宣告一個空的Vue 物件 
  * 組件實例被創建，屬性生效之前 
* Created：這個 Vue 的物件初始化好了，內容的Data ＆ Methods 也好了。 
  * 組件實例已經完全創建，屬性也綁定，但真實DOM 還沒有生成，`$el` 不可使用 
* BeforeMount：把Vue這個初始好的物件，綁到DOM上（存在於記憶體中） 
  * 掛載之前被調用，相關的 render 函數首次被使用 
* Mounted：將DOM渲染至畫面（白話：把DOM放到你的瀏覽器上） 
  * 掛載到實例上調用該 _**hook**_ 
* BeforeUpdate：更新事件 
  * 資料更新前使用，發生在虛擬的DOM 中 
* Updated：更新事件完畢 
* BeforeDestroy：刪除之前（可以控制） 
* Destroyed：刪除之後（無法控制）

## 4.V-Model 原理

參考資料：[IT邦幫忙-Andy Tsai](https://ithelp.ithome.com.tw/articles/10203679?sc=iThelpR)

Ans：

`v-model`：`v-bind` + `@input`

## 5.V-show & V-if 的差別

參考資料：[Gua's Note](https://guahsu.io/2018/08/vue-if-with-vue-show-singleton/)

Ans：

`V-if`：當條件為`True`時，會把內容的DOM渲染出來，如果條件為 `false`，則會把DOM移掉（消失）。並且直到條件變為真，才會開始渲染條件區塊。

`v-show`：一開始就把DOM渲染出來，當條件切換時，只做`Display：none`的切換。（不管條件為何，元素總是會被渲染，只是針對_**CSS**_ 的`Display`做切換。）

## 6.Computed / Watch / Methods 的差異

參考資料：[WJM1818 on OSCHINA](https://my.oschina.net/u/3649083/blog/1560106) 、[IT邦幫忙-Hunterliu](https://ithelp.ithome.com.tw/articles/10192032)

SAME：

1. Watch & Computed：當相依數據發生變化時，所以依賴這個數據的相關數據，會自動變化，也就是自動調用相關的函數去實現數據變動。 
2. 都是以函數為基礎

DIFFERENT：

* Computed： 
  * 資料動，我則變動 
  * 利用Computed的緩存特性，避免每次獲取資料時，都要重新計算。 
* Watch： 
  * 觀察作用，監聽回調、監控數值 
  * 執行非同步、開銷較大的操作時，使用Watch，允許我們執行非同步操作（訪問API），並且可以讓我們在得到最終結果前，_**設置中間狀態**_。 
* Methods： 
  * 需要手動控制，就是資料變了，他不會自動去改 
  * 資料動，觸發了，才變動。

## 7.Computed / Filter 的差異

參考資料：[小狐狸事務所](http://yhhuang1966.blogspot.com/2019/02/vue-computed-filters.html)

Computed：將原始數據，做過篩選顯示。

Filter：可直接於樣板標籤中呼叫並串接，用來把欲輸出之變數再處理。

順序上，應該為Computed -&gt;Filter（先篩選出資料，再對資料做後處理）

## 8.Directive 設計使用

資料來源：[Vue.js 自定義指令](https://cn.vuejs.org/v2/guide/custom-directive.html)

Main：為了讓DOM的功能做一個拓展

## 9.nextTick的使用

資料來源：[知乎-Vue.js$nextTick的一個問題](https://www.zhihu.com/question/50879936)

簡而言之：你現在更新一個東西，但這個更新不會立即執行，必須要等DOM更新後才會執行。

概念：有點像同步與非同步的概念。

流程：

Step1. 同步指令執行完。

Step2. DOM 更新。

Step3. nextTick 這時才更新。

## 10.對SPA頁面的理解，優缺點分別為何？

#### 優點：

* 用戶體驗好、快，內容不需要重新整理，避免了不必要的跳轉和重複渲染 
* 對Server的壓力較小 
* 前後端職責分離，前端進行邏輯，後端負責數據。 
* 利用路由機制來實現HTML每頁的跳轉。

#### 缺點：

* 初次加載耗時多：因為為了實現單頁Web 應用功能及顯示效果、，需要在加載頁面時將JS、CSS統一加載。 
* 前進後退路由管理：所有頁面切換需要自己堆疊管理 
* SEO難度較大：所有內容都在同一個頁面上動態替換顯示，所以在SEO上有著天然的弱勢。

























