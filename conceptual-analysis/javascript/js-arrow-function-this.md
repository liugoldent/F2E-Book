# Arrow Function - This

## 觀念

* arrow function 的 this 是依據環境的父層區域來綁定。意思為arrow function 定義位置的上一層 this 代表誰，arrow function 內的 this 就代表誰

```javascript
var a = 1;
function funcA(){
	console.log(this.a)
    let arrA = ()=> console.log(this.a)
    arrA()
}
let objA = {
    a:2,
	funcA: funcA
}
//直接呼叫的狀況，this 是 window，裡面的 arrow function 也抓到 window
funcA()
// 1
// 1

// 改為透過 objA 去呼叫，this 變成 objA，arrow function 也抓到 objA
objA.funcA()
// 分析過程
// 1. 物件內將 funcA 分配為 funA()
// 2. 為非自己宣告，故可以指向objA
// 2
// 2

```

from [卡斯伯的教學](https://wcc723.github.io/javascript/2017/12/21/javascript-es6-arrow-function/)

```javascript
var name = '全域阿婆'
var auntie = {
  name: '漂亮阿姨',
  callName: function () { 
    // 注意，這裡是 function，以此為基準產生一個作用域
    console.log('1', this.name); // 1 漂亮阿姨
    setTimeout(() => {
      console.log('2', this.name); // 2 漂亮阿姨
      console.log('3', this); // 3 auntie 這個物件
    }, 10);
  },
  callName2: () => { 
    // 注意，如果使用箭頭函式，this 依然指向 window
    console.log('4', this.name); // 4 全域阿婆
    setTimeout(() => {
      console.log('5', this.name); // 5 全域阿婆
      console.log('6', this); // 6 window 物件
    }, 10);
  }
}

auntie.callName();
// 一般function 無異議
auntie.callName2();
// 分析過程：
// 1. 物件內直接宣告箭頭函式 > 指向 window
// 不行，則為window
```

{% hint style="info" %}
不是建立在物件內的函式，不會影響箭頭函式的 this
{% endhint %}

```javascript
var auntie = {
  name: '漂亮阿姨',
  callName () { 
    // 注意，縮寫形式的 function 屬於傳統 function
    setTimeout(() => {
      console.log(this); // auntie 這個物件
    }, 10);
  }
}
auntie.callName();
// 分析過程
// 1. 是由物件內宣告
// 2. 宣告時為正常函式 
// 3. 正常函式內指的 this 為 auntie 
// 4. 故 setTimeout 指向 auntie
```

## 不可使用

### 於 call\(\)、apply\(\)、bind\(\)

from [箭頭函數 Arrow Function](https://ithelp.ithome.com.tw/articles/10195669)

```javascript
let people = {
    name: 'Bob'
}
const fn_arrow = () => {
    console.log(this);
}
const fn = function () {
    console.log(this);
}

fn_arrow.call(people); // 箭頭函數，this 依然還是 window 物件
fn.call(people);  // 一般函數，this 則改變成 people 物件
```

### 於 new 建構函數

### 於 prototype 方法

