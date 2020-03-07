# Expression / Operator part2

## 運算子

資料來源：[重新認識 JavaScript Day8](https://ithelp.ithome.com.tw/articles/10191343)

### 比較運算子

* 一個等於（ `=` ）。賦值 
* 兩個等於（ `==` ）。自動轉型的比較 
* 三個等於（ `===` ）。不會自動轉型的比較 
* 不等於（ `!=` ）。會自動轉型 
* 不等於（ `!==` ）。不會自動轉型

#### 自動轉型的規則

* 如果其中一個為 Boolean，會將 true 轉為數字 1。false 轉為數字 0 
* 字串與數字作比較，字串會先轉為數字 `Number()` 
* 若一個為物件型態，則會用 `valueOf()`，取得基本型別的值。 
* NaN 不等於 NaN 
* 兩個物件比較時，指向同一個_**實體**_才會回傳 `true`

下列範例資料來源：[重新認識JS，Day07](https://ithelp.ithome.com.tw/articles/10191254)

```javascript
//神奇的比較 
false == 0    // true
true == 1     // true

[] == []      // false
[] == ![]     // true

[] == ''      // true
[] == 0       // true

[''] == ''    // true
[0] == 0      // true

[0] == ''     // false
[''] == 0     // true

null == undefined   // true

[null] == ''        // true
[null] == 0         // true

[undefined] == ''   // true
[undefined] == 0    // true
```

### 指派運算子

| 運算子 | 行為 |
| :--- | :--- |
| a += b | a = a + b |
| a  -= b | a = a - b |
| a \*= b | a = a \* b |
| a /= b  | a = a / b |
| a %= b | a = a %  b |

### 逗號運算子

#### 目的：讓逗號分隔運算式可以循序執行（由左至右），並回傳最後一個運算式的值

```javascript
for(let i =1 ,j = 1 ; i < 10 ; i++){
    console.log(i+j)
}

let a = 10 , b = 10
//但記住不等於
let a = b = 10 
//因為這個相等於
let a = 10
b = a > 沒有宣告出 b
```

### 邏輯運算子

* 在 `&&` `||` `!`，其中 `! not` 運算子，會回傳 `true` or `false` 
* 在使用上面三種前首先要知道  


  * `Undefined` 
  * `Null` 
  * 0 / `NaN` 
  * `""` / `''`（空字串） 會轉化為 `false`

* 而其他狀況會轉化為 `true`

範例程式

```javascript
var a = 123;
var b = "abc";
var c = null;
var d = NaN
var e = ""

console.log( a && b );        // "abc"
console.log( a || b );        // 123

console.log( c && a );        // null
console.log( c || b );        // "abc"
console.log( c || a );        // 123
console.log( e && d );        // ""
console.log( e || d );        // NaN
```

* 在處理這些運算子時，會先透過 `ToBoolean` 判斷 `falsy` or `truthy` 
* 對 `&&` 而言，若第一個值轉換為 `true`，則回傳第二個值 
* 對 `||` 而言，若第一個值轉換為 `true`，則會傳第一個值 
* 對 `&&` 而言，若第一個值轉換為 `false`，則回傳第一個值 
* 對 `||` 而言，若第一個值轉換為 `false`，則會傳第二個值

