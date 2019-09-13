# For Loop Effectiveness

此篇主要介紹關於 `for Loop` 的效率

參考文章：[掘金-JS數組循環的性能與效率分析](https://juejin.im/post/5b645f536fb9a04fc9376882)

## 比較組別

### 常見的四種for Loop 

```javascript
//method1
for (let i=0;i<persons.length ; i++){}

//method2
for (let i=0 , len = persons.length ; i<len ; i++){}

//method3
for (let i = 0, person; person = persons[i]; i++) {}

//method4
for (let i = persons.length; i--;) {}
```













