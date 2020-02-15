# Template \(模板方法模式\)

## Code

```javascript
class Beverage {
    constructor({brewDrink, addCondiment}) {
        this.brewDrink = brewDrink
        this.addCondiment = addCondiment
    }
    /* 烧开水，共用方法 */
    boilWater() { console.log('水已经煮沸=== 共用') }
    /* 倒杯子里，共用方法 */
    pourCup() { console.log('倒进杯子里===共用') }
    /* 模板方法 */
    init() {
        this.boilWater()
        this.brewDrink()
        this.pourCup()
        this.addCondiment()
    }
}
/* 咖啡 */
const coffee = new Beverage({
     /* 冲泡咖啡，覆盖抽象方法 */
     brewDrink: function() { console.log('冲泡咖啡') },
     /* 加调味品，覆盖抽象方法 */
     addCondiment: function() { console.log('加点奶和糖') }
})
coffee.init() 
// "水已经煮沸=== 共用"
// "冲泡咖啡"
// "倒进杯子里===共用"
// "加点奶和糖"
```

## 解釋

模板方法由兩部份結構組成，第一部份為抽象父類，第二部份是具體的實現子類。通常在抽象父類中風莊子類的算法框架，包括實現一些公共的方法和封裝子類中所有方法的執行順序。子類通過繼承抽象，也繼承整個算法結構，並且可以選擇重寫父類的方法

## 場景

* 一次性實現一個算法的不變部份，並將可變的行為留給子類來實現
* 子類中公共的行為應該被提出並集中到一個共用父類中，避免代碼重複

## 優點

* 提取了公用的部份，易於維護

## 缺點

* 增加系統複雜度





