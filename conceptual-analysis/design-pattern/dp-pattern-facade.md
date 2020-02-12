# Facade（外觀模式）

資料來源：

* [阿洲的程式教學：表象模式](http://monkeycoding.com/?p=975) 
* [Alex：JS\_Next（線上不公開課程）](https://www.youtube.com/user/achen224)

## 目的

{% hint style="info" %}
提供一個統一的介面，用來存取次系統的一群介面，讓次系統容易使用
{% endhint %}

## **舉例**

* 假設你今天要蛋炒飯，其步驟 
  * 放油 
  * 煎蛋 
  * 放飯＋醬油 
  * 把蛋和飯炒在一起 
* 假設你今天是一個客人，我只需要吃到蛋炒飯就好，我不用知道那麼多 
* 所以我_**只要知道原料**_（油、蛋、醬油、飯）就可以，丟進去後，_**機器自動**_煮。

## Code

### ES5

```javascript
const tomato = function() {
  return "番茄";
};
const egg = function() {
  return "炒蛋";
};

const tomatoEgg = function() {
  return tomato() + egg();
};
console.log(tomato() + egg());
console.log(tomatoEgg());

//以上，使用者只要知道tomato / egg 即可，不用知道那是怎麼排列的
```

### ES6

```javascript
class Facade {
    _get() {
        console.log("current value:" + this.i);
    }
    _set(val) {
        this.i = val;
    }
    _run() {
        console.log("running");
    }
    _jump() {
        console.log("jumping");
    }

    facade(args) {
        this._set(args.val);
        this._get();
        if (args.run) {
            this._run();
        }
    }
}
let fa = new Facade();
fa.facade({ run: true, val: 10 });
//印出 current value:10
//印出 running
```

## 優點

* 減少系統相互依賴 
* 提高靈活性 
* 提高安全性

## 缺點

* 不符合開放封閉原則









