# TypeOf

## JS 內建型別

* 基本型別：
  * number、String、boolean、null、undefined、symbol
* 物件型別
  * 物件及其子型別（陣列、函式、日期）

## JS 基本型別判斷（是檢測「值」的型別）

{% tabs %}
{% tab title="JavaScript" %}
```javascript
console.log(typeof 2)
// number
console.log(typeof 's')
// string
console.log(typeof true)
// boolean
console.log(typeof null)
// object
console.log(typeof undefined)
// undefined
console.log(typeof NaN)
// number
console.log(typeof { a:1})
// object
console.log(typeof [1,2,3])
// object
console.log(typeof function() {})
// function
```
{% endtab %}
{% endtabs %}

## JS 檢測 null 判斷

{% tabs %}
{% tab title="JavaScript" %}
```javascript
console.log("" == false) // true
console.log("" === false) //false

console.log(0 == false) // true
console.log(0 === false) // false

console.log(-0 == false) // true
console.log(-0 === false) // false

console.log(NaN == false) // false
console.log(NaN === false) // false

console.log(null == false) // false
console.log(null === false) // false

console.log(undefined == false) //false
console.log(undefined === false) //false

console.log(null == undefined)  // true
console.log(null === undefined) // false

console.log(!null) // true
console.log(!NaN)  // true
console.log(!undefined) // true

```
{% endtab %}
{% endtabs %}

{% tabs %}
{% tab title="JavaScript" %}
```javascript
// 空陣列
if([]){
  console.log(1)
}
// 空物件
if({}){
  console.log(2)
}
// 空函式
if(function foo(){}){
  console.log(3)
}
// 1
// 2
// 3
```
{% endtab %}
{% endtabs %}

## JS 長度判斷

```javascript
function test (a,b,c){
  console.log(123)
}

const list = [1,2,3,4,5]

console.log('',test.length) 
console.log('',list.length)
// 3
// 5
```

## JS 檢測物件子型別

```javascript
Object.prototype.toString.call([1, 2, 3]) // [object array]
```

## JS new 建構子

```javascript
let a = new Number()
let b = new String()
let c = new Boolean()

console.log(typeof a) // object
console.log(typeof b) // object
console.log(typeof c) // object
```

