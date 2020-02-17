# Interpreter \(解释器模式\)

## Code

```javascript
class Context {
  constructor() {
    this._list = []; // 存放 终结符表达式
    this._sum = 0; // 存放 非终结符表达式(运算结果)
  }

  get sum() {
    return this._sum;
  }

  set sum(newValue) {
    this._sum = newValue;
  }

  add(expression) {
    this._list.push(expression);
  }

  get list() {
    return [...this._list];
  }
}

class PlusExpression {
  interpret(context) {
    if (!(context instanceof Context)) {
      throw new Error("TypeError");
    }
    context.sum = ++context.sum;
  }
}

class MinusExpression {
  interpret(context) {
    if (!(context instanceof Context)) {
      throw new Error("TypeError");
    }
    context.sum = --context.sum;
  }
}

/** 以下是测试代码 **/

const context = new Context();

// 依次添加: 加法 | 加法 | 减法 表达式
context.add(new PlusExpression());
context.add(new PlusExpression());
context.add(new MinusExpression());

// 依次执行: 加法 | 加法 | 减法 表达式
context.list.forEach(expression => expression.interpret(context));
console.log(context.sum);
```

## 核心概念

* 抽象表達 func &gt; 主要有個 `interpret()` 操作 
* Context中，存放文法中各個 `class` 所對應的具體值

## 優點

* 每個規則可以表達為一個類或方法。這些文法互相不干擾，符合封閉原則

## 缺點

* 由於每條文法都需要建構一個類或是方法，文法數量上去後難以維護。並且語句的執行效率低，一直在不停地互相調用

