# Mediator\(中介者模式\)

## Code

```javascript
class A {
    constructor() {
        this.number = 0
    }
    setNumber(num, m) {
        this.number = num
        if (m) {
            m.setB()
        }
    }
}
class B {
    constructor() {
        this.number = 0
    }
    setNumber(num, m) {
        this.number = num
        if (m) {
            m.setA()
        }
    }
}
class Mediator {
    constructor(a, b) {
        this.a = a
        this.b = b
    }
    setA() {
        let number = this.b.number
        this.a.setNumber(number * 10)
    }
    setB() {
        let number = this.a.number
        this.b.setNumber(number / 10)
    }
}

let a = new A()
let b = new B()
let m = new Mediator(a, b)
a.setNumber(10, m)
console.log(a.number, b.number)
b.setNumber(10, m)
console.log(a.number, b.number)

```

## 目的

* 解除物件與物件之間的緊耦合關係。增加一個中介者物件後，所有的相關物件都通過中介者物件來通信，而不是互相引用，所以當一個物件發生改變時，只需要通知中介者物件即可。中介者讓各物件之間耦合鬆散，而且可以獨立地改變他們之間的交互。中介者模式讓網狀的多對多關係變成一對多關係。 
* 類似觀察者模式，但是是單向的，由中介者統一管理

## 場景

* 系物統中物件之間存在比較複雜的引用關係，導致他們之間的依賴關係結構混亂而且難以複用該物件。 
* 想通過一個中間類，來封裝多個類中的行為，而又不想生成太多子類

## 優點

* 使各物件之間耦合鬆散，而且可以獨立地改變他們之間的交互。 
* 中介者和物件一對多的關係取代了物件之間的網狀多對多關係 
* 如果物件之間的複雜耦合度導致維護很困難，而且耦合度隨項目變化增速很快，就需要中介者重構

## 缺點

* 在系統中會新增一個中介者物件，因為物件之間交互的複雜性，轉移成中介者物件的複雜性，使得中介者物件經常是巨大的。中介者物件自身往往就是一個難以維護的對象。

