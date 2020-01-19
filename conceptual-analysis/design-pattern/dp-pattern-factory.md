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

### ES5

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

### ES6

#### 簡單工廠模式

* 建立相似物件時，進行重複性的工作，達到程式碼精簡
* 物件或元件涉及高複雜性
* 須根據不同環境生成物件的時候
* 處理很多共享屬性的小型物件或元件時

```javascript
//Definition of class
class User {    
    constructor(typeOfUser){
        this._canEditEverything = false;        
        if (typeOfUser === "administrator") {               
            this._canEditEverything = true;
        }
    }    get canEditEverything() { return this._canEditEverything; }
}
//Instatiation
let u1 = new User("normalGuy");
let u2 = new User("administrator");
```

#### 工廠方法

* 一個父類別，一個子類別
* 首先建立一個父類別，內要有一個變數，內也要有一個function
* 經由子類別覆寫的方式，建立出新物件，並且可以使用父類別的方法

```javascript
//Class
class User {
    constructor(){
        this._canEditEverything = false;
    }
    get canEditEverything() { return this._canEditEverything; }
}
//Sub-class
class Administrator extends User {
    constructor() {
        super();
        this._canEditEverything = true;
    }
}
//Instatiation
let u2 = new Administrator();
let result = u2.canEditEverything; //true
```

#### 抽象工廠

```javascript
class PorscheCar {  
  constructor(params) {
    this.engine = params.engine;
    this.tyreModel = params.tyreModel;
    this.gears = params.gears;
  }
}

class PorscheCarFactory {  
  createCar(params) {
     return new PorscheCar(params);
  }
}

class FerrariCar {  
  constructor(params) {
    this.engine = params.engine;
    this.tyreModel = params.tyreModel;
    this.gears = params.gears;
    this.turbo = params.turbo;
  }
}

class FerrariCarFactory {  
  createCar(params) {
     return new FerrariCar(params);
  }
}

class CarFactoryImpl {
  constructor() {
    this.porscheCar = new PorscheCarFactory();
    this.ferrariCar = new FerrariCarFactory();
  }

  getPorsche() {
    return this.porscheCar;
  }
  
  getFerrari() {
    return this.ferrariCar;
  }
}

const fact = new CarFactoryImpl();
let params = { engine: "raw", tyreModel: "basic", gears: null };

const concretePorsche = fact.getPorsche().createCar(params);
console.log(concretePorsche);
  
params = { engine: "rawraw", tyreModel: "basic", gears: null, turbo: true };
const concreteFerrari = fact.getFerrari().createCar(params);
console.log(concreteFerrari.turbo);
```

## 優點

* 創建物件的過程複雜，但我們只需要知道結果就好 
* 構造函數和創建者分離，符合封閉原則 
* 一個使用者想要創建一個物件，只要知道其名稱就好 
* 想增加一個產品，只要擴建一個工廠即可

## 缺點

* 添加新產品時，會增加系統複雜度 
* 需要引入抽象層，增加系統的難以理解度

## 例子

* jQuery、Vue非同步組件







  


