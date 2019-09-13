# For Loop Effectiveness

此篇主要介紹關於 `for Loop` 的效率

參考文章：[掘金-JS數組循環的性能與效率分析](https://juejin.im/post/5b645f536fb9a04fc9376882)

## 比較組別

### 常見的幾種 Loop

```javascript
const persons = ['a','b','c','d','e','f']

//method1（普通for循環）
for (let i=0;i<persons.length ; i++){}

//method2（儲存長度）
for (let i=0 , len = persons.length ; i<len ; i++){}

//method3（取值與判斷合併）
for (let i = 0, person; person = persons[i]; i++) {}

//method4（i-- 與判斷合併，反向迭代）
for (let i = persons.length; i--;) {}

//method5（while）
while (i< persons.length){}

//method6（forEach）
persons.forEach((item)=>{})

//method7（map）
persons.map(item=>item)

//method8（for of）
for(let item of Persons){}

```

## 結論

### 比較佔用內存（作者只有比較四種方法）：

* method3 &gt; method2 &gt; method4 &gt; method1

### 比較執行速度（Best to Worse）：

* In Chrome 
  * method2 -&gt; method3 -&gt; method4 -&gt; method1 
* In FireFox 
  * method6 -&gt; method8 -&gt; method7 -&gt; method4 
* In Safari 
  * method7 -&gt; method5 -&gt; method6 -&gt; method4

### 瀏覽器判斷：

* In Chrome：ES6 & Map is _**Worse**_

## 注意

* `for loop`、`while loop`、`for of loop` 可以使用 `break` 跳出 









