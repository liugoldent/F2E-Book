# Array Methods

## Array 常用的屬性/方法

參考資料：[MDN Array](https://developer.mozilla.org/zh-TW/docs/Web/JavaScript/Reference/Global_Objects/Array)

### 屬性：

* `length`：可以知道這個陣列長度為何

```text
var clothing = ['shoes', 'shirts', 'socks', 'sweaters'];

console.log(clothing.length);
// expected output: 4
```

### 方法：

* `concat()`：用來合併兩個或多個陣列。此方法_**不會**_改變現有的陣列。

```javascript
var array1 = ['a', 'b', 'c'];
var array2 = ['d', 'e', 'f'];

console.log(array1.concat(array2));
// expected output: Array ["a", "b", "c", "d", "e", "f"]
```

* `forEach()`：將陣列中的每個元素，皆傳入並執行給定的函式一次（ _**依序**_）。

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

* `join()`：將陣列中所有的元素連結，並且合併成一個字，最後_**回傳字串**_。

```javascript
var elements = ['Fire', 'Air', 'Water'];

console.log(elements.join());
// expected output: "Fire,Air,Water"

console.log(elements.join(''));
// expected output: "FireAirWater"

console.log(elements.join('-'));
// expected output: "Fire-Air-Water"
```

* `map()`：map 會_**建立一個新陣列**_，而其內容為原本陣列，經由函式運算過後所得到的結果。

```javascript
var array1 = [1, 4, 9, 16];

// pass a function to map
const map1 = array1.map(x => x * 2);

console.log(map1);
// expected output: Array [2, 8, 18, 32]
```

* `shift()`：移除第一個元素，並回傳被刪除的那個第一個元素。

```javascript
var array1 = [1, 2, 3];

var firstElement = array1.shift();

console.log(array1);
// expected output: Array [2, 3]

console.log(firstElement);
// expected output: 1
```

* `pop()`：移除最後一個元素，並回傳被刪除的最後一個元素。

```javascript
var plants = ['broccoli', 'cauliflower', 'cabbage', 'kale', 'tomato'];

console.log(plants.pop());
// expected output: "tomato"

console.log(plants);
// expected output: Array ["broccoli", "cauliflower", "cabbage", "kale"]
```

* `push()`：添加一個或多個元素至陣列的末端，並且回傳陣列的新長度。

```javascript
var animals = ['pigs', 'goats', 'sheep'];

console.log(animals.push('cows'));
// expected output: 4

console.log(animals);
// expected output: Array ["pigs", "goats", "sheep", "cows"]
```

* `reverse()`：反轉一個陣列。_**注意：原本陣列也會被反轉**_。

```javascript
var array1 = ['one', 'two', 'three'];

var reversed = array1.reverse(); 
console.log('reversed: ', reversed);
// expected output: Array ['three', 'two', 'one']

/* Careful: reverse is destructive. It also changes
the original array */ 
console.log('array1: ', array1);
// expected output: Array ['three', 'two', 'one']
```

* `slice()`：回傳一個新陣列物件，此陣列為選擇之 _**`begin`**_ 至 _**`End-1`**_ 的拷貝，而原陣列不會被修改。

```javascript
var animals = ['ant', 'bison', 'camel', 'duck', 'elephant'];

console.log(animals.slice(2));
// expected output: Array ["camel", "duck", "elephant"]

console.log(animals.slice(1, 5));
// expected output: Array ["bison", "camel", "duck", "elephant"]
```

* `splice()`：刪除已有的元素，並加入新元素來改變一個陣列的內容_**（注意位置與輸入數字）**_。

```javascript
var months = ['Jan', 'March', 'April', 'June'];
months.splice(1, 0, 'Feb');
// inserts at index 1
console.log(months);
// expected output: Array ['Jan', 'Feb', 'March', 'April', 'June']

months.splice(4, 1, 'May');
// replaces 1 element at index 4
console.log(months);
// expected output: Array ['Jan', 'Feb', 'March', 'April', 'May']

months.splice();
//可以讓陣列更新,並且不刪掉任何一個元素
```

* `sort()`：排列一個陣列。

```javascript
var months = ['March', 'Jan', 'Feb', 'Dec'];
months.sort();
console.log(months);
// expected output: Array ["Dec", "Feb", "Jan", "March"]

var array1 = [1, 30, 4, 21, 100000];
array1.sort();
console.log(array1);
// expected output: Array [1, 100000, 21, 30, 4]
```

* `findIndex（）`：找出條件之索引，無則為 _**-1**_

```javascript
var array1 = [5, 12, 8, 130, 44];
console.log(array1.findIndex((element) => element>13));
//expected output : 3
//notice 找到第一個，則結束此迴圈
```

* `find（）`：找出條件之值，無則為 _**undefined**_

```javascript
var array1 = [5, 12, 8, 130, 44];

var found = array1.find(function(element) {
  return element > 10;
});

console.log(found);
// expected output: 12
```











