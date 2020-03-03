# By ref or by value

## 基本型別

* 傳值 
* let a = 1 &gt; let b =a 時，電腦會在記憶體中新增一個新值，讓後來的變數指向新的值

```javascript
let a = 1
let b = a
b++

console.log('',a,b)
// 1 , 2 > 基本型別傳值
```

## 物件型別

* 傳址 
* 變數指向電腦記憶體中的相同的位址

```javascript
let obj1 = { v1 : 1}
let obj2 = { v2 : 1}
console.log(obj1 == obj2) // false
console.log(obj1 === obj2) // false
// 因為是兩個獨立存在的實體

let obj3 = obj1
obj3.value = 2

console.log(obj1) //{ v1: 1, value: 2 }
console.log(obj3) //{ v1: 1, value: 2 }
console.log(obj1 == obj3) // true
console.log(obj1 === obj3) // true

obj1 = {}

console.log(obj1) // 又重新分配給 obj1 一個新的位置 > {}
console.log(obj3) // 但是obj3 沒有接到通知，所以還是{ v1: 1, value: 2 }
```

### 物件型別之淺拷貝（Shallow Copy）

#### 現在產生一個問題為，那個想要複製物件給物件怎麼辦？用等於就變成一次動到位置內的物件，故要使用淺拷貝

* 物件的淺拷貝 
  * `object.assign(target,sources)`

```javascript
// target 目標物件
// sources 
let obj1 = { v1 : 1}
let obj2 = Object.assign({},obj1)

console.log('',obj2) // { v1 : 1}
console.log(obj1 == obj2) // false

```

* 物件的淺拷貝 
  * 在一個空物件中，使用 `...` 展開運算子 展開物件

```javascript
let obj1 = { v1 : 1}
let obj2 = { ...obj1}

console.log('',obj2) // { v1 : 1}
console.log(obj1 == obj2) // false

```

### 陣列型別的淺拷貝

* `slice()`：使用 slice\(0\)，達到拷貝效果 
* `concat()` 
* `forEach + push()` 
* `map()` 
* `filter()` 
* `...` 展開運算子

```javascript
// slice(0)
let array1 = [1,2,3]
let array2 = array1.slice(0)

console.log(array2) // [1,2,3]
console.log(array1 == array2) //false

// concat
let array1 = [1,2,3]
let array2 = [].concat(array1)

console.log(array2)
console.log(array1 == array2)

// forEach + push
let array1 = [1,2,3]
let array2 = []

array1.forEach(item => {
  array2.push(item)
})

console.log(array2)
console.log(array1 == array2)

// map
let array1 = [1,2,3]
let array2 = array1.map(item => {
  return item
})

console.log(array2)
console.log(array1 == array2)

// filter
let array1 = [1,2,3]
let array2 = array1.filter(item => {
  return true
})

console.log(array2)
console.log(array1 == array2)

// ...
let array1 = [1,2,3]
let array2 = [...array1]

console.log(array2)
console.log(array1 == array2)

```

### 但今天若是陣列內有物件 or 物件內有物件，則要使用深拷貝

```javascript
let obj1 ={
  foo:10,
  bar:{
    a:2,
    b:3
  }
}

let obj2 = {...obj1}

console.log(obj1 === obj2) // false
console.log(obj1.bar == obj2.bar) 
// true , 注意外層已經被拷貝，故為false, 而內層因為是傳址，故還是 true
```

#### 解決方案

* `JSON.parse(JSON.stringify(obj1))`

```javascript
let obj1 ={
  foo:10,
  bar:{
    a:2,
    b:3
  }
}

let obj2 = JSON.parse(JSON.stringify(obj1))

console.log(obj1 === obj2) // false
console.log(obj1.bar == obj2.bar) // false


- - - - - - - - - - - - - - 


// 但如果物件內有 function undefined Symbol > 忽略
// NaN Infinity -Infinity > 被轉成 null
let obj1 ={
  foo:10,
  bar:{
    a: Infinity,
    b: NaN,
    c: function(){},
  }
}

let obj2 = JSON.parse(JSON.stringify(obj1))

console.log(obj1 === obj2) // false
console.log(obj1.bar == obj2.bar) // false
console.log(obj1.bar) //{ a: Infinity, b: NaN, c: [Function: c] }
console.log(obj2.bar) // {a : null , b: null}

```



