# Class

## Code

```javascript
class Order {
    constructor(data){
        this.data = data
    }
    get price (){
        console.log(2)
        let b = this.basePrice
        console.log('bbbb',b)
    }
    get basePrice (){
        console.log('',333)
        return 3
    }
    set SetPrice(data){
        this.data = data
    }
}

let a = new Order(1)
console.log('',a.data) // 1
a.SetPrice = 7
console.log('',a.data) // 7
```

## 解釋

* 使用 get &gt; 可以直接呼叫其 function。ex：`a.basePrice`。而不用 `a.basePrice()`
  * _**不可**_帶值給get的 function 
* 使用 set &gt; 可以再設定其function的值。呼叫方式：`a.SetPrice`。不用 `a.SetPrice()`
  * 可帶值給set 的 function 
* 如果沒有 get or set，則呼叫要使用 `a.basePrice()` or `a.SetPrice()`。

