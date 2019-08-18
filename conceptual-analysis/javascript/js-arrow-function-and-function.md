# Arrow Function And Function

參考資料：

* [it邦幫忙：卡斯伯-箭頭函式](https://ithelp.ithome.com.tw/articles/10192732) 
* [PJCHENder 談談JS的 Arguments](https://pjchender.blogspot.com/2016/04/javascriptparameterargumentsspread.html)

## Both：

* 可以傳入參數 
* 有大括號包起來

## Arrow Function（Feature）

1. 沒有`Arguments` 參數  
  
   `Arguments`：就是`parameters`的意思，但`arguments` 會包含所有你放入`function`的參數值。  


   ```javascript
   const ArrowFunction = () => {
     console.log(arguments); 
   }
   ArrowFunction(10, 50, 100, 50, 5, 1, 1, 1, 500);
   // arguments is not defined

   const GeneralFunction = function () {
     console.log(arguments); 
   }
   GeneralFunction(10, 50, 100, 50, 5, 1, 1, 1, 500);
   // OK
   ```

2. 綁定的 `this` 不同  


   * 傳統函式：依照呼叫方法而定 
   * 箭頭函式：依照綁定到其定義所在的物件（充滿了陷阱）



   ```javascript
   var name = "全域阿婆";
   var auntie = {
     name: "漂亮阿姨",
     callName: function() {
       // 注意，這裡是 function，以此為基準產生一個作用域
       console.log("1", this.name); // 1 漂亮阿姨
       setTimeout(() => {
         console.log("2", this.name); // 2 漂亮阿姨
         console.log("3", this); // 3 auntie 這個物件
       }, 10);
     },
     callName2: () => {
       // 注意，如果使用箭頭函式，this 依然指向 window
       console.log("4", this.name); // 4 全域阿婆
       setTimeout(() => {
         console.log("5", this.name); // 5 全域阿婆
         console.log("6", this); // 6 window 物件
       }, 10);
     }
   };
   auntie.callName();
   auntie.callName2();
   ```

3. 不可使用的情況：`apply` , `call` , `bind`  
  
   `this` 在 _**Arrow Function**_ 中是被綁定的，所以套用 `call` 時無法修改`this`。  


   ```javascript
   let family = { ming: '小明' } 
   const func = () => { console.log(this); } 
   const func2 = function () { console.log(this); } 
   func.call(family); // 箭頭函式的情況，this 依然是 window 
   func2.call(family); // 一般函示 this 則是傳入的物件傳統函式：依照呼叫方法而定

   //{}
   //{ ming: '小明' } 
   ```

4. 不能用在建構式  
  
   由於`this`是在物件下建立，所以箭頭函式_**不能**_像 _**function**_ 一樣作為建構式的函式（簡單來說_**不能被new**_）  


   ```javascript
   const PhoneTemplate = (man, modal) => {
     this.man = man;
     this.modal = modal;
   }
   const sonyPhone = new PhoneTemplate('Father', 'Z100');
   // Wrong
   ```

5. 無法使用於 DOM 事件監聽  因為`this` 指向所_**建立的物件**_上，如果用於_**監聽DOM**_，也會_**指向 Window**_，會無法使用。 
6. Prototype 中使用 this  在原型上新增一個箭頭函式，這個`this`會指向_**全域**_ 



  


















