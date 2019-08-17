# TypeOf And InstanceOf

## Both：

{% hint style="success" %}
能避免程式碼異常，為一種較嚴謹的處理方式。
{% endhint %}

## TypeOf：

* 用於判斷參數是什麼類型的方法。

```javascript
console.log(typeof 123); //number
console.log(typeof 'jartto'); //string
console.log(typeof !!'0'); //boolean
console.log(typeof new Function()); //function
console.log(typeof name); //undefined
```

* 但也要注意暫時性死區的問題

```javascript
console.log(typeof x);
let x;
```

{% hint style="warning" %}
較適用於基本類型的數據
{% endhint %}

{% hint style="danger" %}
不適用於物件、陣列、null 的判斷
{% endhint %}

## InstanceOf：

* `instanceof` 用來判斷 A 是否為 B 的實例，表達式為 `A instanceof B`，如果「_**是**_」返 回`true`，_**否**_則返回`false`。 
* 有點_**A是不是B**_的概念。但是是物件、陣列型的。

```javascript
[] instanceof  Array ; //true
 ({}) instanceof  Object ; //true 
new  Date () instanceof  Date ; //true
```

## 擴展：

#### 分析 \[ \]、Array、Obj 的關係

* 從`instanceof`，能夠判斷出 `[].proto` 指向 `Array.prototype`，而 `Array.prototype.proto`又指向`Obj.prototype`，最終`Obj.prototype.proto`指向了`null`，原型鏈結束。













