# Adapter（適配器模式）

## 目的

{% hint style="success" %}
用來解決兩個接口不兼容的問題，由一個物件來包裝不兼容的物件
{% endhint %}

## Code

```javascript
    class Adapter {
        specificRequest () {
            return '德国标准插头';
        }
    }
    // 适配器对象，对原来不兼容对象进行包装处理
    class Target {
        constructor () {
            this.adapter = new Adapter();
        }
        request () {
            const info = this.adapter.specificRequest();
            console.log(`${info} - 转换器 - 中国标准插头`)
        }
    }
    const target = new Target();
    console.log(target.request()); // 德国标准插头 - 转换器 - 中国标准插头

```

## 優點

* 讓兩個沒有關聯的類，一起運行 
* 提高了類的復用 
* 適配物件、庫、數據

## 缺點

* 可考慮重構，讓這個Code變好。 
* 需要創建額外的對象，不能直接使用，會有一定的開銷

## 場景

* Vue Computed



