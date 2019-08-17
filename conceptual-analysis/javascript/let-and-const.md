# Let And Const

以下會比較ES6後出現的 `Let` and `Const`

* In ES5 Only `var` 
* In ES6：`let`、`const`、`var`

參考資料：

1. [it邦幫忙-eyesofkids：let與Const](https://ithelp.ithome.com.tw/articles/10185142) 
2. [Medium卡斯伯：ES6開始的新生活](https://wcc723.github.io/javascript/2017/12/20/javascript-es6-let-const/) 
3. [ITREAD：let 與 const 用法這些就夠了](https://www.itread01.com/xpyqp.html)

## Basic：

* `let`：用來宣告_**變數**_，所宣告的變數只在`let`命令所在的_**程式碼區塊內**_有效。 
* `const`：用來宣告_**常數**_，所謂常數就是_**不可以更改**_的變數。 
* `let`、`const`：具有區塊作用域（_**Block Scope**_）。

## Let：

1. `let` 宣告的變數只在宣告時所在的_**程式碼區塊內**_有效。  


   ```javascript
   {
   let a=10;
   }
   ```

2. _**有變數提升**_現象，但因暫時性死區會變成_ReferenceError_。（變數提升：Hoisting）。  
  
   這邊要特別提出一個參考資料：[let聲明會提升嗎？](https://zhuanlan.zhihu.com/p/27558914)  


   ```javascript
   //var 情況
   console.log(foo); //Undefined
   var foo=2;

   //let 情況
   console.log(bar); //ReferenceError
   let bar=2;
   ```

3. 暫時性死區（_**TDZ**_）：在程式區塊內，使用let命令宣告變數之前，該變數都不可使用。  


   ```javascript
   {
   tmp='abc'; //ReferenceError
   console.log(tmp); //ReferenceError

   let tmp; //暫時性死區結束。
   console.log(tmp); //Undefined
   }
   ```

4. `let` 不允許在同一個作用域內_**重複**_宣告變數。  


   ```javascript
   //報錯
   function fun(){
   let a=10;
   let a=1;
   }
   ```

5. 在`for`迴圈的時候  


   ```javascript
   for(let i=0;i<10;i++){
    //.....
   }
   console.log(i);
   // ReferenceError：i is not defined
   ```

   ```javascript
   for(let i=0;i<3;i++){
    let i='abc';
    console.log(i);
   }
   // abc
   // abc
   // abc
   // ()小括號內的是父作用域
   // {}大括號內的是子作用域
   ```

## Const：

1. const 宣告一個只讀的常量，一經宣告，無法再改變。  


   ```javascript
   const PI =3.1415;
    PI=3;//Error
   ```

2. 一但宣告變數，·必須_**立刻初始化**_（賦值），只宣告不賦值，報錯。  


   ```javascript
   const foo;
   //SyntaxError: Missing initializer in const declaration
   ```

3. 一樣只在作用域內有效（請參考`let`的第一點）。 
4. `const` 保證的是變數指向的那個記憶體_**位址不得改變**_。  


   ```javascript
   const foo = {};
   foo.prop =123; //ok
   foo = {}; //TypeError：'foo' is read-only
   ```

   * 對於數值、字串、布林，值是儲存於變數指向的那個記憶體位址。 
   * 對於複合型別的資料（物件、陣列），變數指向的記憶體位址，是一個指向實際資料的指標，const 只能保證這個指標是固定的（即總是指向一個固定的位址），至於其指向的資料結構是否可變，就無法控制。

## Classic Test：

```javascript
for (let i = 0; i < 10; i++) {
  console.log(i);
  setTimeout(function () {
    console.log('這執行第' + i + '次');
  }, 0);
}
```

與

```javascript
for (var i = 0; i < 10; i++) {
  console.log(i);
  setTimeout(function () {
    console.log('這執行第' + i + '次');
  }, 0);
}
```

## Coding Style

{% hint style="info" %}
不要再使用`var` 宣告變數，改用 `let` 與 `const`，而且優先使用`const`，除非需要指定值才用 `let`
{% endhint %}

{% hint style="info" %}
減少使用逗號來宣告多個變數。`eg. let a=1,b=2;`
{% endhint %}

{% hint style="info" %}
於合理位置，放置變數宣告。（通常我都會集中在最上面）
{% endhint %}













