# Promise

## 基礎的

```javascript
const myFirstPromise = new Promise((resolve, reject) => {
  resolve(someValue);         // 完成
  reject("failure reason");   // 拒絕
});
```

## 若想要順序執行func &gt; 使用 then

```javascript
function funcA(){
  return new Promise(function(resolve, reject){
    window.setTimeout(function(){
      console.log('A');
      resolve('A');
    }, (Math.random() + 1) * 1000);
  });
}

function funcB(){
  return new Promise(function(resolve, reject){
    window.setTimeout(function(){
      console.log('B');
      resolve('B');
    }, (Math.random() + 1) * 1000);
  });
}

function funcC(){
  return new Promise(function(resolve, reject){
    window.setTimeout(function(){
      console.log('C');
      resolve('C');
    }, (Math.random() + 1) * 1000);
  });
}
```

## 順序執行

```javascript
funcA().then(funcB).then(funcC);
```

一次全部執行

```javascript
// funcA, funcB, funcC 的先後順序不重要
// 直到這三個函式都回覆 resolve 或是「其中一個」 reject 才會繼續後續的行為

Promise.all([funcA(), funcB(), funcC()])
       .then(function(){ console.log('上菜'); });
```

