# THINK-2

THINK篇主要述說在寫Vue時的基本觀念

而大部分的資料都可以從官網獲得：

* [掘金](https://juejin.im/post/5d59f2a451882549be53b170) 
* [Vue 官網 - 教程](https://cn.vuejs.org/v2/guide/)

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

## 11.Class 和 Style 如何動態綁定

#### 皆可使用 _**物件語法**_ 與 _**陣列語法**_ 來進行動態綁定

```javascript
//class
//物件
<div v-bind:class="{ active: isActive, 'text-danger': hasError }"></div>
data: {
  isActive: true,
  hasError: false
}
//陣列
<div v-bind:class="[isActive ? activeClass : '', errorClass]"></div>
data: {
  activeClass: 'active',
  errorClass: 'text-danger'
}
```

```javascript
//style
//物件
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
data: {
  activeColor: 'red',
  fontSize: 30
}
//陣列
<div v-bind:style="[styleColor, styleSize]"></div>
data: {
  styleColor: {
     color: 'red'
   },
  styleSize:{
     fontSize:'23px'
  }
```

## 12.理解Vue的單向數據流

* 所有prop 都使其父子之間形成一個單向往下的綁定，父級prop的更新會向下流動到子組件中，但是反過來則不行，這樣可以防止子組件意外改變父級組件的狀態。 
* 所以當父組件改變時，子組件會刷新成新的值。而我們只能透過 `$emit` 發送一個定義事件，通知父組件修改，然後再傳進來（也就是子組件不應該修改值）。

```javascript
props: ['initialCounter'],
props: ['size']
data: function () {
  return {
    counter: this.initialCounter
    //如果要修改東西時
    //return this.size.trim().toLowerCase()
  }
}
```

## 13.讓Vue 必定能偵測到資料變化的方式

#### 無法監測到的狀況：

* 使用索引值，設置一個陣列項目時。ex：`vm.items[IndexOfItem] = newValue` 
* 直接修改陣列長度時。ex：vm.items.length = newLength

#### 解決第一個問題的方式：

```javascript
// Vue.set
//陣列 -> 索引 -> 新的值
Vue.set(vm.items, indexOfItem, newValue)
// vm.$set，Vue.set的一个别名
vm.$set(vm.items, indexOfItem, newValue)
// Array.prototype.splice
vm.items.splice(indexOfItem, 1, newValue)
```

#### 解決第二個問題的方式：

```javascript
vm.items.splice(newLength)
```

#### 更多參考資料：[為什麼畫面沒隨資料更新而更新](https://pjchender.blogspot.com/2017/05/vue-vue-reactivity.html)

##  









































