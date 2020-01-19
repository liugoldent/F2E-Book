# Singleton（單例模式）

資料來源：

* [it邦幫忙：jilin178-單例模式](https://ithelp.ithome.com.tw/articles/10202016) 
* [阿洲的程式教學：單例模式](http://monkeycoding.com/?p=969)

## Purpose

* 保證一個類別僅有一個實例，並提供一個存取他的全域存取點。 
* 除了第一次的新增外，之後皆使用第一次產生的對象。 
* 透過閉包隔離實體避免被直接操作。 
* 需要時才建立，所以不會像全域變數一開始設定即佔一個資源。（但每次都需要判斷）

## Conceptual

* 例如瀏覽器的_**Window**_，只需要一個這樣的物件 
* 一個網頁，需要被重複共用的東西 
  * Loading Page 
  * 警告視窗

## Code

### ES5

```javascript
const Singleton = (function() {
  let instance = null;
  return function() {
    if (!instance) {
      instance = new Noraml();
    }
    return instance;
  };
})();

let SO1 = new Singleton();
SO1.count++;
let SO2 = new Singleton();

console.log(SO1.count);//1
console.log(SO2.count);//1
console.log(SO1.count === SO2.count);//true

//兩個是一樣的物件
```

### ES6



```javascript
//流程
//按下按鈕時，去呼叫這個class的 function
//於此同時會去判斷是否被實體化
//如果還沒，就返回一個new的實體化
//如果已經，就返回實體化的物件
<button id="loginBtn">登录</button>
    <script>
        const btn = document.getElementById('loginBtn');
        btn.addEventListener('click', function() {
            loginLayer.getInstance();
        }, false);
        
        class loginLayer {
            constructor() {
                this.instance = null;
                this.init();
            }
            init() {
                var div = document.createElement('div');
                div.classList.add('login-layer');
                div.innerHTML = "我是登录浮窗";
                document.body.appendChild(div);
            }
            static getInstance() {
                if(!this.instance) {
                    this.instance = new loginLayer();
                }
                return this.instance;
            }
        }
```

### ES6（In Node.js）

```javascript
//export 模式 for node
class Singleton {
  constructor () {
    if (!Singleton.instance) {
      Singleton.instance = this
    }
    // Initialize object
    return Singleton.instance
  }
  // Properties & Methods
}


const instance = new Singleton()
Object.freeze(instance)


export default instance
```

## 優點

* 劃分命名空間，減少全局變量 
* 增強模組性，放在全域變量下，便於維護 
* 只會實例化一次

## 缺點

* 由於是提供一種單點的訪問，所以可能導致模組間的強耦合，而不利於單元測試。

## 場景

* VueX、登陸框











