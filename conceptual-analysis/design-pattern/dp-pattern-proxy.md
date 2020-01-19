# Proxy（代理模式）

## 目的

{% hint style="success" %}
代理者是指一個類別可以作為其它東西的接口。代理者可以作任何東西的接口：網絡連接、內存中的大對象、文件或其它昂貴或無法複製的資源。
{% endhint %}

## Code

```javascript
class Flower {}
// 源对象
class Jack {
    constructor (target) {
      console.log('1')
        this.target = target;
        //這個target 等於 proxyObj
    }
    sendFlower (target) {
            console.log('2')
        const flower = new Flower();
        this.target.receiveFlower(flower)
    }
}
// 目标对象
class Rose {
    receiveFlower (flower) {
            console.log('3')
        console.log('收到花: ' + flower)
    }
}
// 代理对象
class ProxyObj {
    constructor () {
                  console.log('4')
        this.target = new Rose();
    }
    receiveFlower (flower) {
                  console.log('5')
        this.sendFlower(flower)
    }
    sendFlower (flower) {
                        console.log('6')
        this.target.receiveFlower(flower)
    }
}
const proxyObj = new ProxyObj();
const jack = new Jack(proxyObj);
jack.sendFlower(proxyObj); 
```

### 流程

* 4、1、2、5、6、3

## 優點

* 能將代理對象與被調用對象隔離，降低系統耦合度。對在客戶端與目標對象之間，起到一個中介作用，可以保護目標對象。 
* 可以擴展目標對象的功能，通過修改代理對象就可以達到，符合封閉原則。

## 缺點

* 處理請求速度有差，非直接訪問存在開銷。

## 不同點

* 裝飾器模式：擴展功能，原有功能不變，且可以直接使用 
* 代理模式：顯示原有功能，但是是經過限制之後的。

