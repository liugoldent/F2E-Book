# For Loop Effectiveness

此篇主要介紹關於 `for Loop` 的效率

參考文章：[掘金-JS數組循環的性能與效率分析](https://juejin.im/post/5b645f536fb9a04fc9376882)

## 比較組別

### 常見的幾種 Loop

```javascript
const persons = ['a','b','c','d','e','f']

//method1
for (let i=0;i<persons.length ; i++){}

//method2
for (let i=0 , len = persons.length ; i<len ; i++){}

//method3
for (let i = 0, person; person = persons[i]; i++) {}

//method4
for (let i = persons.length; i--;) {}

//method5
while (i< persons.length){}

//method6
persons.forEach((item)=>{})

//method7
persons.map(item=>item)

//method8
for(let item of Persons){}

```

## 結論

### 比較佔用內存（作者只有比較四種方法）：

* method3 &gt; method2 &gt; method4 &gt; method1

### 比較執行速度（少秒速至多秒速）：

* In Chrome 
  * method2 -&gt; method3 -&gt; method4 -&gt; method1 
* In FireFox 
  * method6 -&gt; method8 -&gt; method7 -&gt; method4 
* In Safari 
  * method7 -&gt; method5 -&gt; method6 -&gt; method4











