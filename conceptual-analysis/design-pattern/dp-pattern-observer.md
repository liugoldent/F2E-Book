# Observer（觀察者模式）

## 目的

{% hint style="success" %}
建立一種一對多的相依關係，當一個物件的狀態發生改變時，所有相依他的物件都將得到通知，並且自動更新。
{% endhint %}

## Code

```javascript

// 观察的主题（目标对象），相当于发布者
class Subject {
  constructor() {
    this.subs = [];
    this.state = "张三";//触发更新的状态
  }
  //新增两个对于name的操作 获取/更新
  getState() {
    return state;
  }
  setState(state) {
    if (this.state === state) {
      console.log('不能设为之前的name，无效');
      return;
    }
    this.state = state;
    this.notify(); // 有更新，触发通知！【原本手动触发通知的，现在根据数据变化来触发】
  }
  addSub(sub) {
    this.subs.push(sub);
    console.log(this.subs)
  }
  removeSub(sub) {
    const idx = this.subs.findIndex(i => i === sub);
    if (idx === -1) {
      console.log('不存在该观察者');
      return;
    }
    this.subs.splice(idx, 1);
  }
  notify() {
    this.subs.forEach(sub => {
      sub.update();// 与观察者原型方法update对应！
    });
  }
}

// 观察人，相当于订阅者
class Observer {
  update() {
    console.log('update');
  }
}

// 测试代码
const subject = new Subject();
const ob = new Observer();
const ob2 = new Observer();
ob2.update = function () { //修改update方法，实现不同逻辑
  console.log('laifeipeng');
}

//目标添加观察者了
subject.addSub(ob);
subject.addSub(ob2);

//目标发布消息调用观察者的更新方法了
// subject.notify(); // 不使用手动触发，通过内部状态的设置来触发
subject.setState('李四');
// update
// laifeipeng

subject.setState('李四');
// 不能设为之前的name，无效


```

### 流程

* 首先各自都new 出一個實體 
* 再把ob / ob2 增加到原始 subject 中，讓 subject 可以追蹤 
* 所以當subject.setState之後，底下的 ob / ob2 都獲得通知，更新狀態。

## 優點

* 支持簡單的廣播通信，自動通知已經訂閱的物件 
* 目標物件與觀察者之間的抽象耦合關係，能夠單獨擴展與重用 
* 增加靈活性 
* 觀察者：解耦，讓耦合的雙方都依賴於抽象，而不是依賴於實體，使得各自變化不會影響另一邊的邊畫。

## 缺點

* 過度使用，導致物件與物件間的聯繫弱化，導致程式難以維護和理解

