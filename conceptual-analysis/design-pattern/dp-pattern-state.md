# State（狀態模式）

## 目的

{% hint style="success" %}
關鍵是區分事物內部的狀態，事物內部狀態往往會帶來事物的行為改變，允許物件在內部狀態發生改變時，改變他的行為
{% endhint %}

## Code

```javascript
// 红灯
class RedLight {
    constructor (state) {
        this.state = state;
    }
    light () {
        console.log('turn to red light');
        this.state.setState(this.state.greenLight)
    }
}
// 绿灯
class greenLight {
    constructor (state) {
        this.state = state;
    }
    light () {
        console.log('turn to green light');
        this.state.setState(this.state.yellowLight)
    }
}
// 黄灯
class yellowLight {
    constructor (state) {
        this.state = state;
    }
    light () {
        console.log('turn to yellow light');
        this.state.setState(this.state.redLight)
    }
}
class State {
    constructor () {
        this.redLight = new RedLight(this)
        this.greenLight = new greenLight(this)
        this.yellowLight = new yellowLight(this)
        this.setState(this.redLight) // 初始化为红灯
    }
    setState (state) {
        this.currState = state;
    }
}
const state = new State();
state.currState.light() // turn to red light
setInterval(() => {
    state.currState.light() // 每隔3秒依次打印红灯、绿灯、黄灯
}, 3000)

```

## 優點

* 定義了狀態與行為之間的關係，封裝在一個類裡面，更直觀清晰，方便修改 
* 狀態與狀態間，行為與行為間彼此獨立不受干擾 
* 用物件代替字串來紀錄當前狀態，使得狀態切換更一目瞭然

## 缺點

* 會在系統中定義許多狀態類 
* 邏輯分散

