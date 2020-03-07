# Function

## 基本宣告函式

```javascript
function square(number){
    return number * number
}
// 在() 中的為，參數(Arguments)
// 在{} 中的為，函式功能內部的主要區塊
```

## 定義函式的方式

* 函式宣告（同上） 
* 函式運算式

```javascript
const NewNumber = function(number){
    return number * number
}
// 此稱匿名函式
```

* 透過 new Function建立函式（運作效能較差）

```javascript
const NewNumber = new Function('number' , return number * number)
```

## 變數的有效範圍（Scope）

* ES6前，JS 變數有效範圍的最小單位是以 function 

```javascript
var x = 100
function dosomething(y){
    console.log(x) // 輸出 100 > 因為function 內沒有，所以向外找
    console.log(y) // 輸出 10 > 傳入的參數
    return x+y
}
console.log(dosomething(10)) // 110
console.log(x) // 輸出 100
- - - - - - - - - - - - 
var x = 100
function dosomething(y){
  var x = 3
    console.log(x) // 輸出 3 > 因為 function 內有，所以使用這個 3
    console.log(y) // 輸出10
    return x+y
}
console.log(dosomething(10)) // 13
console.log( x ) // 100
- - - - - - - - - - - - 
var x = 100
function dosomething(y){
  x = 3
    console.log(x) // 3
    console.log(y) // 10
    return x+y
}
console.log(dosomething(10))
console.log(x) // 3 ：因為裡面的 x 設定為3，等於重新把外面的值賦值
```

* ES6後，有 `let` `const` 分別定義變數與常數。他們的 scope 是用 `{}` 來切分的

## 關於函數的 Hoisting

{% page-ref page="js-hoisting.md" %}



#### 

