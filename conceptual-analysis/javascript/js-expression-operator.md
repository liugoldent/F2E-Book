# Expression / Operator

## JS語法：敘述句/運算式/運算子

## 敘述句：執行某個動作。

* 例如：宣告、賦值、迴圈、`if` 判斷式

## 運算式：產生一個值

* var a = 10 \* 10  ， `=` 右邊就是運算式

## 運算子：

### 特殊加法

```javascript
// +
Infinity+Infinity = Infinity
-Infinity+-Infinity = -Infinity
Infinity-Infinity = NaN

// -
Infinity-Infinity = NaN
-Infinity-Infinity = -Infinity
Infinity--Infinity = Infinity 

// 互相抵銷則為 NaN
// 互相相加 會為 - or + Infinity
```

```javascript
// if 有 NaN > 加起來必定NaN
10 + NaN = NaN
Infinity + NaN = NaN
```

#### 字串轉型

* `number` / `boolean` / `obj` &gt; 會自動 `.toString()` 
* 而 `null` `undefined` 會轉為 `'null'` / `'undefined'`

```javascript
100 + '100' = 200
100 + 'ABC' = '100ABC'
'ABC' + 'DEF' = 'ABCDEF'
100 + {} = 100 [object Object]

// undefined 也會轉為字串 ，而相加也會再轉為 NaN
123 + undefined = NaN // Number(undefined) = NaN
'abc' + undefined = 'abcundefined'

// null 也會轉為數字 = 0
123 + null = 123 // Number(null) = 0 
'123' + null = '123null'
```

#### 運算式相加為由左到右 & 先乘除後加減

```javascript
let a = 1000
let b = 50
let c = 'Hi 你好' + a + b // 'Hi 你好100050'
```

### if 為減號（-）

* 減法運算時，`string` `boolean` `undefined` `null` 碰到減號 會透過 `Number()`轉型

```javascript
// - 號
100 - '50' = 50
100 - 'abc' = NaN // 因為轉字串為???，但還是數字，故為NaN
// boolean 會轉成 0 or 1
100 - false = 100
100 - true = 99
100 - undefined = NaN // Number(undefined) = NaN
100 - null = 100 // Number(null) = 0
100 - {} = NaN
```

#### 若為物件型別

* 如果是物件型別，物件則會利用 `valueof()` 方法求得值（待`prototype` 敘述）

### 乘法

```javascript
// 若為 NaN > 乘出來必定 NaN
// 如果其中一個不為數字，會先 Number()
100 * '10' = 1000
100 * abc = NaN
100 * true = 100
100 * false = 0
100 * {} = NaN
```

### 除法

```javascript
// if 有一方為 NaN 則結果必為NaN
1 / 0 = Infinity
-1 / 0 = -Infinity
0 / 0 = NaN
```

### 餘數

```javascript
// 當左方為 Infinity like > 必定為 NaN
Infinity / 0 = NaN
// 當右方為 Infinity > 則結果為左方
```

### 算術運算子：強制轉型

```javascript
console.log(+10) // 10
console.log(+'ABC') // NaN  也會轉為數字，但為NaN
```

### 遞增與遞減

```javascript
let a = 10 
let b = 10
console.log(a++) // （a++為後做）我下定義 這個 a 要加，但是還沒做
console.log(a) // 因為後做+1 > 就印出了 11
console.log(++b) // (先做+1)，所以印出11
console.log(b) // 已經做了，所以就是11
```

### 遞增遞減相乘

```javascript
// ++ 在前代表回傳先做的值
// ++ 在後代表回傳現在的值
let a = 10
console.log(++a*a) // 121
```

