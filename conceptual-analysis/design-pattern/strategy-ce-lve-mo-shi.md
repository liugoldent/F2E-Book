# Strategy（策略模式）

資料來源：

* [阿洲的程式教學-策略模式](http://monkeycoding.com/?p=958) 
* [Summer - Strategy 策略模式](http://cythilya.blogspot.com/2015/07/javascript-design-pattern-strategy.html) 
* [it邦幫忙：jlin178-策略模式](https://ithelp.ithome.com.tw/articles/10202419)

## Purpose

* 將變動的部分、各種方法_**封裝**_起來 
* 使用物件，而非使用判斷式（`switch`）（判斷式違反開放封閉原則） 
* 針對介面寫程式，不是針對實踐寫程式 
* 多用合成，少用繼承。 
* 原則：將不變的部分和變化的部分分開

## Conceptual

* 今天有個百貨做折扣  


  * 低階會員：95折 
  * 中階會員：85折 
  * 高階會員：7折

  

* 分年終 
  * 資深F2E：薪水\*4 
  * 中階F2E：薪水\*3 
  * 低階F2E：薪水\*2 
* 依照不同程度，做出策略

## Code

（下面兩段是不同人寫的Code，但你可以發現架構非常像）

（建議可以參考看看 [it邦幫忙：jlin178-策略模式](https://ithelp.ithome.com.tw/articles/10202419) 的表單使用）

```javascript
//演算法
var strategies = {
	'S': function(salary) {
		return salary * 4;
	},
	'A': function(salary) {
		return salary * 3;
	},
	'B': function(salary) {
		return salary * 2;
	}
};

//使用它
var calcBonus = function(performance, salary) {
	return strategies[performance](salary);
};
console.log(calcBonus('S', 100));
```

```javascript
const strategies = {
  1: function(amount) {
    return amount * 0.95;
  },
  2: function(amount) {
    return amount * 0.85;
  },
  3: function(amount) {
    return amount * 0.85;
  }
};

const discountStrategy = function(level, amount) {
  return strategies[level](amount);
};

console.log(discount(1, 1000));
```















