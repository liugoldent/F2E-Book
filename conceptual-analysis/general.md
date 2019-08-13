# General

## 1. Cookie、LocalStorage、SessionStorage的差異

資料來源：[Charlie Chen on Medium](https://medium.com/@jscinin/javascript-cookie-localstorage-sessionstorage-%E4%B8%89%E7%A8%AE%E5%B7%AE%E7%95%B0-fe7f38260439)

| 特性 | Cookie | LocalStorage | SessionStorage |
| :--- | :--- | :--- | :--- |
| 數據的生命週期 | 由服務器生成，可設置失效時間。如果在瀏覽器端生成Cookie，默認是關閉瀏覽器後失效。 | 除非被清除，否則永久保存。 | 僅在當前有效，入關閉頁面或瀏覽器後被清除。 |
| 存放數據的大小 | 4 KB 左右 | 5 MB | 同左 |
| 與服務器端的通性 | 攜帶於HTTP 中，如果使用Cookie 保存過多數據，會導致性能問題。 | 僅在客戶端（Web）中保存，不參與和服務器的通信。 | 同左 |
| 易用性 | 需要程序員自行封裝，原生的Cookie 接口並不好。 | 原生接口可以接受，亦可再次封裝來對物件和陣列有更好的支持。 | 同左 |

## 2. Array 常用的屬性/方法

### 屬性：

* `length`：可以知道這個陣列長度為何

```text
var clothing = ['shoes', 'shirts', 'socks', 'sweaters'];

console.log(clothing.length);
// expected output: 4
```

### 方法：

* `concat()`：用來合併兩個或多個陣列。此方法不會改變現有的陣列。

```javascript
var array1 = ['a', 'b', 'c'];
var array2 = ['d', 'e', 'f'];

console.log(array1.concat(array2));
// expected output: Array ["a", "b", "c", "d", "e", "f"]
```

* `forEach()`：將陣列中的每個元素，皆傳入並執行給定的函式一次。

```javascript
var array1 = ['a', 'b', 'c'];

array1.forEach(function(element) {
  console.log(element);
});

// expected output: "a"
// expected output: "b"
// expected output: "c"
```

* `indexof()`：回傳給定元素於陣列中第一個被找到的索引，若不存在則回傳為`-1`。

```javascript
var beasts = ['ant', 'bison', 'camel', 'duck', 'bison'];

console.log(beasts.indexOf('bison'));
// expected output: 1

// start from index 2
console.log(beasts.indexOf('bison', 2));
// expected output: 4

console.log(beasts.indexOf('giraffe'));
// expected output: -1
```

* `join()`：將陣列中所有的元素連結，並且合併成一個字，最後回傳字串。

```javascript
var elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());
// expected output: "Fire,Air,Water"

console.log(elements.join(''));
// expected output: "FireAirWater"

console.log(elements.join('-'));
// expected output: "Fire-Air-Water"
```















