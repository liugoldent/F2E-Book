# Decorator（裝飾者模式）

## 目的

{% hint style="success" %}
動態的給某個物件增加一些額外的職責，一種實現繼承的替代方法
{% endhint %}

{% hint style="success" %}
在不改變原本物件的基礎上，通過其進行包裝與擴展，使原有物件可以滿足用戶得更複雜需求，也不會影響到原本的物件
{% endhint %}

## Code

```javascript
class MacBook {
    cost() {
        return 997;
    }
    screenSize() {
        return 11.6;
    }
}

function Memory(macbook) {
    let v = macbook.cost();
    macbook.cost = function() {
        return v + 75;
    };
}
// Decorator 2
function Engraving(macbook) {

    let v = macbook.cost();
    macbook.cost = function() {
        return v + 200;
    };
}
// Decorator 3
function Insurance(macbook) {
    let v = macbook.cost();
    macbook.cost = function() {
        return v + 250;
    };
}
let mb = new MacBook();
Memory(mb);
Engraving(mb);
Insurance(mb);
console.log(mb.cost());// Outputs: 1522
console.log(mb.screenSize());// Outputs: 11.6
```

## 優點

* 只關心自身的核心任務，實現解耦 
* 方便動態擴充功能，比繼承多了更多的靈活性

## 缺點

* 多層的話會較複雜 
* 常常引入小物件，看起來相似，實際功能卻不對，讓我們的架構變得複雜

