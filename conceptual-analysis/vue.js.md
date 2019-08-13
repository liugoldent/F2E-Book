# Vue.js

此篇主要述說在寫Vue時的基本觀念

而大部分的資料都可以從官網獲得：[Vue官網-教程](https://cn.vuejs.org/v2/guide/)

## 1.為何使用V-for 時，必須加上Key值？

參考資料：[CSDN-「Vue v-for 中的key」](https://blog.csdn.net/qq_35285627/article/details/81012902)

```text
<div v-for="item in items" :key="item.id">
```

Ans：  
為了給Vue一個提示，方便它能追蹤每個節點的身份。並且理想的Key是唯一的值。  
並且為了避免錯誤的渲染。

## 2.Vue 傳遞資料的方式

參考資料：[VueJS-元件-Component-之間資料傳遞的方式](https://kuro.tw/posts/2018/08/22/VueJS-%E5%85%83%E4%BB%B6-Component-%E4%B9%8B%E9%96%93%E8%B3%87%E6%96%99%E5%82%B3%E9%81%9E%E7%9A%84%E6%96%B9%E5%BC%8F/)

Ans：

1. Data 
2. 父給子：Props / 子給父：Emit   
3. 兄弟組建之間傳遞：Bus

## 3.Vue 生命週期

參考資料：[Vue生命週期函數](https://blog.csdn.net/chen1042246612/article/details/89190217)

Ans：

* BeforeCreate：宣告一個空的Vue 物件 
* Created：這個 Vue 的物件初始化好了，內容的Data ＆ Methods 也好了。 
* BeforeMount：把Vue這個初始好的物件，綁到DOM上（存在於記憶體中） 
* Mounted：將DOM渲染至畫面（白話：把DOM放到你的瀏覽器上） 
* BeforeUpdate：更新事件 
* Updated：更新事件完畢 
* BeforeDestroy：刪除之前（可以控制） 
* Destroyed：刪除之後（無法控制）

## 4.V-Model 運作方式

參考資料：

## 5.V-show & V-if 的差別

## 6.Computed / Watch / Methods 的差異

