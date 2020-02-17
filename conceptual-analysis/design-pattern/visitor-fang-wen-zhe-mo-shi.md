# Visitor \(訪問者模式\)

## Code

```javascript
// 访问者  
class Visitor {
    constructor() {}
    visitConcreteElement(ConcreteElement) {
        ConcreteElement.operation()
    }
}
// 元素类  
class ConcreteElement{
    constructor() {
    }
    operation() {
       console.log("ConcreteElement.operation invoked");  
    }
    accept(visitor) {
        visitor.visitConcreteElement(this)
    }
}
// client
let visitor = new Visitor()
let element = new ConcreteElement()
elementA.accept(visitor)
```

## 目的

* 表示一個作用於某物件結構中的各元素操作。它使你可以在不改變個元素的前提下定義做用於這些元素的操作

## 場景

* 物件結構中物件對應的類很少改變，但經常需要在此物件結構上定義新的操作 
* 需要對一個物件結構中的物件進行很多不同的並且不相關的操作，而需要避免讓這些操作汙染這些物件的類，也不希望在增加新操作時修改這些類

## 優點

* 符合單一職責 
* 擴展與靈活性

## 缺點

* 具體元素對訪問者公布細節，違反最小知識原則 
* 違反依賴反轉原則，依賴了具體類，沒有依賴抽象 
* 具體元素變得更加困難

