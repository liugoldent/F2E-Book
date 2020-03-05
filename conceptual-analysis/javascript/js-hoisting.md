# Hoisting

{% hint style="info" %}
所謂的輸出 undefined 而非輸出 Reference a is not defined &gt; 稱為 hoisting
{% endhint %}

## 一般情況

```javascript
// example 1
console.log(a) // ReferenceError: a is not defined
// 完全沒宣告 > 合理
```

```javascript
// example 2
console.log(a) // undefined -> 下面的變數提升上來了
var a

// 想像成
var a
console.log(a) 
```

```javascript
// example 3
console.log(a) // undefined -> 但有賦值,值並不會提升
var a = 5 

// 想像成
var a 
console.log(a)
a = 5
```

## function 傳入參數的 hoisting

```javascript
function test(v){
  console.log(v) // 8
  var v = 5
}
test(8)

//可以想像成

function test(v){
  var v = 8 
  var v
  console.log(v) // 所以輸出8
  v = 5
}
test(8)
```

## function 的 hoisting 優先權

```javascript
console.log(a) // function a 因為 function 優先於 變數

var a = 5
function a(){}

```

## 如果沒有 hoisting 

* **變數一定要先宣告才能用 &gt; ok** 
* **一定要先宣告函式才能用 &gt; not ok** 
* **沒有辦法 function 互相呼叫**

## 深度了解

文章連結：[TechBridge 技術共筆部落格 - hoisting](https://blog.techbridge.cc/2018/11/10/javascript-hoisting/)

#### 剖析hoisting

* 函數執行時，會產生所謂的EC（_**Execution context**_）環境，這環境會儲存這個 function 內所需要的所有資訊，這函數需要什麼就去 EX 拿就對了。 
* 每個 EC 有相對應的變數空間物件稱 VO（_**variable object**_），在內宣告的變數跟函式都會被加進去，如果有參數，那參數也會加到 VO 內 
  * 對於 js 而言，var a = 10  
    * 首先分成左半邊 var a &gt;  VO 去新增一個屬性叫做 a，如果沒有這個屬性，就讓它 undefined。 
    * 再來看到右半邊 a = 10  &gt; 去 VO 裡面找到 a 這個屬性，找到後設定為 10
      * 啊如果找不到，就利用 scope chain 向上找，如果找不到最後就拋錯

```javascript
// scope chain
const v = 1 // let or var > same
function test(a){
  console.log(v) // 1
  let b = 2
  console.log(b) // 2
}

test(3)

```

```javascript
// example 1 > VO的作法
function test(a,b,c){}
test (10)

// VO 環境（這邊會發現參數為第一優先順序）
{
    a:10,
    b:undefined,
    c:undefined
}

```

```javascript
// example 2 > VO的權重
function test(a){
    function a(){}
}
test(10)
// VO 環境
{
    a: function a 
}
```

### 如果在VO 內，已經有這個屬性了，那值不會被覆寫掉

```javascript
//  如果在 VO 內，已經有這個屬性了，那值不會被改變
function test (a){
    console.log(a)
    var a = 3
}
test(4)
// VO 環境
{
  a = 4 // 傳參數進去， a就是等於 4了，就算 function 裡有也不會被改變
}
// function 角度
function test(a){
    var a = 4 // 這行是想像
    console.log(a) // 所以這邊對於 函式來說看到是這樣子
    var a = 3
}
```

```javascript
// 所以在這裡面第一個 10 沒問題，而二個 輸出 3 是因為又在宣告一次，故輸出3
function test(a){
    console.log(a) //10
    var a = 3
    console.log(a) // 3
}
test(10)
```

## Temporal Dead Zone

所謂的「暫時性死區」，就是「提升之後」至「賦值之前」這段期間

for `const` & `let`

在 let & const 這兩個部分，也存在著 hoisting，只是結果與 var 不同

如果是 `var` &gt; 會報 undefined

如果是 `let` or `const` &gt; 會報 錯誤

```javascript
function test() {
  var a = 1; // c 的 TDZ 開始
  var b = 2;
  console.log(c) 
  // 如果是 const or let 就會報錯
  // 如果是 var 就會 undefined
  if (a > 1) {
    console.log(a)
  }
  const c = 10 // c 的 TDZ 結束
}
test()

```

而TDZ 是一種時間的概念

在執行時，如果這個變數還沒有被賦值，就是會報錯（`const` & `let`）

而如果是 `var` 就是 undefined

```javascript
function test() {
  yo() // c 的 TDZ 開始
  let c = 10 // c 的 TDZ 結束
  function yo(){
    console.log(c) //這邊會報錯，因為在執行當下 c 還未被賦值
  }
}
test()
```

