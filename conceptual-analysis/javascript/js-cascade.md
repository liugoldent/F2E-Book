# Cascade

## 解釋

* 類似方法鏈，可以不用一直呼叫一個物件的方法，而是用鏈結式的方法去達到目的 
* Cascade / Fluent Interface，這樣方式可以做出方便容易閱讀，而且一口氣把要做完的事寫在一起。

## 一般的Code

```javascript
var calNum = function(num){
  this.num = num;

  this.add = function(newNum) {
    this.num += newNum;
  };

  this.sub = function(newNum) {
    this.num -= newNum;
  };

  this.multi = function(newNum) {
    this.num *= newNum;
  };

  this.division = function(newNum){
    this.num /= newNum;
  };
};

a.add(100);
console.log( a.num );   // 200

a.sub(50);
console.log( a.num );   // 150

//這邊呼叫兩次兩次才達到目的
```

## Cascade Style Code

```javascript
class calNum {
  constructor(num){
    this.num= num ;
  }

  add(newNum) {
    this.num += newNum;
    return this;
  }

  sub(newNum) {
    this.num -= newNum;
    return this;
  }

  multi(newNum) {
    this.num *= newNum;
    return this;
  }

  division (newNum){
    this.num /= newNum;
    return this;
  }
};
let a = new calNum(10)
a.add(10).sub(5).multi(5)
console.log(a)

//console出75
//這邊順便改成使用class的寫法
```

