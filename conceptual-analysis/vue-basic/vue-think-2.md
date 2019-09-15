# THINK-2

THINK篇主要述說在寫Vue時的基本觀念

而大部分的資料都可以從官網獲得：

* [掘金](https://juejin.im/post/5d59f2a451882549be53b170) 
* [Vue 官網 - 教程](https://cn.vuejs.org/v2/guide/)

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

## 14.Vue 父組件與子組件生命週期執行順序

* 加載渲染過程 
  * 父 BeforeCreate、Created、beforeMount 
  * 子 BeforeCreate、Created、beforeMount 
  * 子 Mounted、父 Mounted 
* 子組件更新過程 
  * 父 BeforeUpdate 
  * 子 BeforeUpdate、Updated 
  * 父 Updated 
* 父組件更新過程 
  * 父 BeforeUpdate、Update 
* 銷毀過程 
  * 父 BeforeDestroy 
  * 子 BeforeDestroy、Destroyed 
  * 父 Destroyed

## 15. 在哪些生命週期中可以使用 非同步請求

* 可於 Created、BeforeMount、Mounted 中進行使用，因為在這三個函數中，data 已經創建，而文獻中建議於Created中使用非同步請求。 
* 原因： 
  * 更快獲取後端數據，減少頁面 Loading 時間 
  * SSR 不支持 BeforeMount、Mounted 這些函數，所以放在 Created中有一致性。

## 16.何時可以訪問操作 DOM

* 在 Mounted 中，可以開始操作 DOM。

## 17.父組件監聽子組件的生命週期

* 利用 `@hook` 監聽

```javascript
//  Parent.vue
<Child @hook:mounted="doSomething" ></Child>

doSomething() {
   console.log('父组件監聽到 mounted 鉤子函數 ...');
},
    
//  Child.vue
mounted(){
   console.log('子组件觸發 mounted 鉤子函数 ...');
},    
    
// 以上輸出顺序為：
// 子组件觸發 mounted 鉤子函数 ...
// 父组件監聽到 mounted 鉤子函数 ...
// 另外如 created、updated 也都可以監聽     
```

## 18.Keep-alive

* 為一個 Vue 內置的組件，可以使其組件保留狀態，避免重新渲染 
* 一般結合路由和動態組件一起使用，用於緩存組件。 
* 提供 include & exclude 屬性，兩者都支持字符串或正規表達式 
  * include 只有名稱匹配的或被緩存 
  * exclude 表示任何名稱匹配的都 _**不會**_ 被緩存 
  * exclude 優先級比 include 高 
* 分別對應兩個鉤子函數 
  * Activated：keep-alive 啟動時調用。 
  * Deactivated：keep-alive 停用時調用。

## 19.組件中的 Data 為何是一個函數？

* 因為組件是拿來復用的。而且如果組件中的 Data 是一個物件，那麼作用域將會_**沒有隔離**_。 
* 如果組件中的 Data 是一個函數，那麼每個實例可以維護一份_**被返回對象的獨立拷貝**_，所以實例之間的Data 屬性值不會互相影響。 
* 另外提到 _new Vue_ 中的實例，因為不會被復用，故不存在引用對象的問題。

## 20.



































