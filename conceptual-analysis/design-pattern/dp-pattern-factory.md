# Factory（工廠模式）

資料來源：

* [Summer-Design Pattern：Factory（JS）](http://cythilya.blogspot.com/2015/06/javascript-design-pattern-factory.html) 
* [阿洲的程式教學（C++）](http://monkeycoding.com/?p=967)

## Purpose

* 建立物件，通常實作為一個Class，或Class 內的靜態方法。 
* 作用為：  


  * 對於建立相似的物件，以進行重複性的工作，達到程式碼精簡的目的。 
  * 提供一個無需事先知道，用明確型別建立物件的方式。

## Conceptual

* 我們可以建立一個工廠（披薩店） 
  * 這個披薩店有：進行烘烤 
  * 這個披薩店有：烤完，運送給客人 
* 今天假設你點了_**夏威夷披薩**_，流程： 
  * 進行烘烤。 
  * 烤完，運送給客人。 
* 今天假設你點了_**鮪魚披薩**_，流程： 
  * 進行烘烤。 
  * 烤完，運送給客人。 
* 重點：將重複的行為給包裝起來，變成一個工廠，很像API。

## Code

資料來源：[Alex-JS\_Next](https://www.youtube.com/channel/UCEL8871qFEakpqYpwBSjHNA)

```javascript
const RamenOtaku = function(type) {
  if (typeof RamenOtaku[type] !== "function") {
    throw {
      name: "訂餐失敗",
      message: "查無品項"
    };
  }
  return new RamenOtaku[type]();
};

const RamenOtakuShiromaru = function() {
  this.name = "Shiromaru Ramen";
  this.taste = "good to eat";
};

RamenOtakuShiromaru.extend(RamenOtaku);

RamenOtaku.prototype.eat = function() {
  return `${this.name} is ${this.taste}.`;
};
RamenOtaku.shiromaru = RamenOtakuShiromaru;

//RamenOtaku：建立工廠
//RamenOtakuShiromaru：建立產品
//產品為工廠的 extend
//工廠底下建立一個方法
//設定這個工廠底下的shiromaru為RamenOtakuShiromaru
//注意RamenOtakuShiromaru內又有自身的function

//這邊有個Extend函數，是筆者的上課老師自行定義，故在這邊沒有顯示。
```

















  


