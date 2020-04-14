# This

## 觀念

* this 會因執行的環境與上下文 context 不同，而有不同的結果 
  * this. 不等於 function。代表的是 func 執行時所屬的物件。

## 重新指向 this

文章來源：[卡斯伯-JS的this到底是誰](https://wcc723.github.io/javascript/2017/12/12/javascript-this/)

這邊要注意的是 `setTimeout` 通常會指向全域

```javascript
function callName() {
  console.log('區域', this.name);
  var that = this;
  setTimeout(function () {
    console.log('全域', this.name);
    console.log('區域', that.name);
  }, 10);
}

var name = '全域阿婆';
var auntie = {
  name: '漂亮阿姨',
  callName: callName  
  // 這裡的 function 指向全域的 function，但不重要
}

auntie.callName();
```

## 強制指定this的方式

* 在JS中，有強制指定this的方式，分別是 `call()`、`apply()`、`bind()` 
* `bind()` 
  * 會強制將 `()` 內的物件指定 this 上  
  * 可以想像 function在執行時，「暫時」把他掛在某個物件下

```javascript
var obj = {
  x: 123
};

var func = function () {
  console.log(this.x);
};

func();            // undefined
func.bind(obj)();  // 123
```

* `call()` & `apply()` 
  * 作用相同，差別在於傳入參數的方式不同

```javascript
function func( arg1, arg2, ... ){
  // do something
}

func.call( context, arg1, arg2, ... ); // call 逗點隔開
func.apply( context, [ arg1, arg2, ... ]); // 傳入整個陣列作為參數
```

* bind / call / apply 的差異 
  * `bind()`，會在呼叫前先綁定某個物件，使它不管怎麼被呼叫，都能有固定的 this。尤其是在 callback function 這種場景，可以想像為先綁定好 this，然後讓 func在需要時才被呼叫的類型。 
  * `call()` / `apply()`，是使用在 context較常變動的場景，依照呼叫時的需要帶入不同的物件作為該func 的 this，在呼叫當下就立即執行。

## this 與前後文綁定的基本原則

### 預設綁定

* 在普通、未經修飾的情況下被呼叫，this 自動指定到全域物件。 
* 但若是 _**'use strict'**_ ，`this` 綁定至全域物件的行為，會轉變為 `undefined`

### 隱含式綁定

* 決定 this 的關鍵在於 func 被呼叫的時機點

```javascript
function func() {
  console.log( this.a );
}

var obj = {
  a: 2,
  foo: func
};

func();       // undefined > this 綁到 window > 故 undefined
obj.foo();    // 2 > this 綁到 obj
```

```javascript
function func() {
  console.log( this.a );
}

var obj = {
  a: 2,
  foo: func
};

obj.foo();  // 2

var func2 = obj.foo;
func2();    // undefined > 因為func2() 是被 windows 所呼叫
```

### 顯示綁定

* 透過 bind\(\) / call\(\) / apply\(\) 綁定

### new 關鍵字綁定

* 會產生一個新物件 
* 這個新建構的物件會被設定為那個 func 的 this 綁定目標，也就是 this 會指向新建構的物件

```javascript
function foo(a) {
  this.a = a;
}

var obj = new foo( 123 );
console.log( obj.a );      // 123
// ES6 的寫法請參考 OOP部分
```

### this 的判斷步驟

1. 這個 func 是不是被 `new` 出來的，若是，則 `this` 就是這個被 `new` 的物件 
2. `call()` / `apply()` / `bind()`的方式呼叫，則 `this`就是被指定的物件 
3. 這個 func 被呼叫時，是否存在於某個物件，若是，那 `this` 就是那個物件。 
4. 若沒有滿足以上，則此 func 的 `this` 必定就是_**全域物件**_，在嚴格模式下，則是 `undefined`

