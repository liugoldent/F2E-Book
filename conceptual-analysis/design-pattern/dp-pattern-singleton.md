# Singleton（單例模式）

資料來源：

* [it邦幫忙：jilin178-單例模式](https://ithelp.ithome.com.tw/articles/10202016) 
* [阿洲的程式教學：單例模式](http://monkeycoding.com/?p=969)

## Purpose

* 保證一個類別僅有一個實例，並提供一個存取他的全域存取點。 
* 除了第一次的新增外，之後皆使用第一次產生的對象。 
* 透過閉包隔離實體避免被直接操作。 
* 需要時才建立，所以不會像全域變數一開始設定即佔一個資源。（但每次都需要判斷）

## Conceptual

* 例如瀏覽器的_**Window**_，只需要一個這樣的物件 
* 一個網頁，需要被重複共用的東西 
  * Loading Page 
  * 警告視窗

## Code

```javascript
const Singleton = (function() {
  let instance = null;
  return function() {
    if (!instance) {
      instance = new Noraml();
    }
    return instance;
  };
})();

let SO1 = new Singleton();
SO1.count++;
let SO2 = new Singleton();

console.log(SO1.count);//1
console.log(SO2.count);//1
console.log(SO1.count === SO2.count);//true

//兩個是一樣的物件
```

















