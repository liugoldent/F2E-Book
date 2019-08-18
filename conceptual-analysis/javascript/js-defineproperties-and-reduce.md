# DefineProperties And Reduce

## WHY

#### 特別提出這兩個方法，是因為在上課時，聽到這兩個方法是現在Obj & Array 最好用的方法，故特別提出

資料來源：

* [MDN 中文 DefineProperties](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Object/defineProperty) 
* [MDN 中文 Reduce](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array/Reduce) 
* [Fred's blog。上手使用JS的Map、Reduce](http://fred-zone.blogspot.com/2017/01/javascript-mapreduce.html)

## DefineProperties（For Obj）

* 可以定義新的 or 修改已存在物件的屬性，_**並回傳**_修改過後的物件。 
* 注意，也可以設定  
  * `writable：true / false`（是否可被覆寫） 
  * `get`（唯讀不可寫） 
  * `set`（唯寫不可讀） 
  * `enumerable`（是否顯示） 
  * 用這個方法，可以 _**操作function**_ 得到額外通知。

### DefineProperties Demo

```javascript
let obj = {};
Object.defineProperties(obj, {
  property1: {
    value: 1,
    writable: true,
  },
  property2: {
    value: 'Hello',
    writable: false,
  },
  // etc. etc.
});
console.log(obj.property1); //1
console.log(obj.property2); //Hello
```

### DefineProperty Demo

```javascript
const object1 = {};

Object.defineProperty(object1, 'property1', {
  value: 42,
  writable: false
});
//writable：false，不可被覆寫
object1.property1 = 77;
// throws an error in strict mode

console.log(object1.property1);
// expected output: 42
```

### DefineProperties Combine Demo

```javascript
let a = {
  name: "Liu",
  age: 30
};
Object.defineProperties(a, {
  name: {
    writable: false
  },
  age2: {
    enumerable: true,
    get() {
      console.log("get age");
      return this.age;
    },
    set(val) {
      console.log("set age");
      this.age = val;
    }
  }
});
a.name = "XXX";
a.age2 = 35;
console.log(a);

//console.log 呼叫a
//a去defineProperties裡面找
//用function 可以拿到額外通知
//輸出{ name: 'Liu', age: 35, age2: [Getter/Setter] }

```

## Reduce（For Array）

* `Reduce`方法，對數組中的每個元素，執行您所定義的函數

```javascript
arr.reduce(
    callback
    (accumulator, currentValue[, index[, array]])
    [, initialValue]
    )
```

* _Callback_：我們定義的函數 __
* _Accumulator_（**acc**）：累計器 
* _Current Value_（**cur**）：當前值 
* _Current Index_（**idx**）：當前索引 
* _Source Array_（**src**）：源數組 
* _initialValue_：初始設定值 

### MDN Code1

```javascript
const array1 = [1, 2, 3, 4];
const reducer = (accumulator, currentValue) => accumulator + currentValue;

// 1 + 2 + 3 + 4
console.log(array1.reduce(reducer));
// expected output: 10

// 5 + 1 + 2 + 3 + 4
console.log(array1.reduce(reducer, 5));
// expected output: 15

// reducer是要執行的函式
// 「5」是初始值
```

### MDN Code2

```javascript
//Do Sum
var sum = [0, 1, 2, 3].reduce(function (accumulator, currentValue) {
  return accumulator + currentValue;
}, 0);
//初始值設定為0

var total = [ 0, 1, 2, 3 ].reduce(
  ( acc, cur ) => acc + cur, 5
);
//初始值設定為5
```

### MDN Code3（Obj）

```javascript
var initialValue = 0;
var sum = [{x: 1}, {x:2}, {x:3}].reduce(
    (accumulator, currentValue) => accumulator + currentValue.x
    ,initialValue
);

console.log(sum) //  6
```















