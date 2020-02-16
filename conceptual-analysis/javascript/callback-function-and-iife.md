# CallBack Function & IIFE

參考資料：重新認識JS：Day18

## Callback 

同步、非同步

同步：Sync &gt; 按部就班的做事 &gt; 只有一個跑道，要過終點一個一個來

非同步：Async &gt; 同時做事 &gt; 多個跑道，三位跑者，可以一起跑

### 基本知識

{% hint style="success" %}
一個函式被觸發了，才去被動地執行：我們可以說這是一個Callback Function
{% endhint %}

### 範例

* 在Async Await & Promise 出現之前，我們想要確保每個函式照順序去做，是用Callback Func。但若像以下傳入狀況，當系統一大，就會造成Callback Hell

```javascript
// 為了確保先執行 funcA 再執行 funcB
// 我們在 funcA 加上 callback 參數
var funcA = function(callback){
  var i = Math.random() + 1;

  window.setTimeout(function(){
    console.log('function A');

    // 如果 callback 是個函式就呼叫它
    if( typeof callback === 'function' ){
      callback();
    }

  }, i * 1000);
};

var funcB = function(){
  var i = Math.random() + 1;

  window.setTimeout(function(){
    console.log('function B');
  }, i * 1000);
};

// 將 funcB 作為參數帶入 funcA()
funcA( funcB );
```

### Callback Hell

```javascript
getData(function (a) {
  getMoreData(a, function (b) {
    getMoreData(b, function (c) {
      getMoreData(c, function (d) {
        getMoreData(d, function (e) {
          ...
        });
      });
    });
  });
});
```

## IIFE（立即被呼叫的函式）

### 問題

* 錯誤的 console.log跑法

```javascript
// 假設想透過迴圈 + setTimeout 來做到
// 每秒鐘將 i 的值 console 出來

for( var i = 0; i < 5; i++ ) {
  window.setTimeout(function() {
    console.log(i);
  }, 5000);
}
//5
//5
//5
//5
//5
```

* 因為 JS 切分變數的有效範圍最小單位為Function
* 而JS是非同步語言，所以執行上面的for，不會等setTimeout，而是執行階段就一次跑完，會讓 i = 5 
* 流程： for 迴圈跑完 &gt; setTimeout 執行（而那時的 i = 5 ）（為啥會五次，因為setTimeout 跑了五次）

### 解決方法

{% hint style="success" %}
利用 IIFE 在宣告的當下執行，之後不會再呼叫的特性
{% endhint %}

```javascript
for( var i = 0; i < 5; i++ ) {

  // 為了凸顯差異，我們將傳入後的參數改名為 x
  // 當然由於 scope 的不同，要繼續在內部沿用 i 也是可以的。
  (function(x){
    window.setTimeout(function() {
      console.log(x);
    }, 1000);
  })(i);

}
// 立刻執行把 i 放到 console.log(x) 中
// 一般函式改成 IIFE > 正常 func 先用小括號包起來，再執行自己
```

## ES6的 let const

可以解決上述 定義域的問題



