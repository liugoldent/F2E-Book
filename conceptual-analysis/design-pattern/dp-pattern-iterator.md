# Iterator（迭代器模式）

## 目的

{% hint style="success" %}
做遍歷不同的集合，提供一個統一的接口，從而支持同樣的算法在不同的集合結構下進行操作。
{% endhint %}

{% hint style="success" %}
提供一種方法順序，訪問物件中的各個元素，而無需暴露出物件的內部
{% endhint %}

## Code

### 外部迭代

```javascript
class Iterator {
  constructor (list) {
    this.list = list;
    this.index = 0;
  }
  next () {
    if (this.hasNext()) {
      return this.list[this.index++]
    }
    return null;
  }
  hasNext () {
    if (this.index === this.list.length) {
      return false;
    }
    return true;
  }
}
const arr = [1, 2, 3, 4, 5, 6];
const ite = new Iterator(arr);

while(ite.hasNext()) {
  console.log(ite.next()); // 依次打印 1 2 3 4 5 6
}

```

## 優點

* 訪問一個聚合對象，不用暴露他的內部表示

## 使用時機

* 對於集合內部的結果常常變化，不想暴露其結構，又想讓大家可以看到其中的元素，可以使用此迭代器模式。

