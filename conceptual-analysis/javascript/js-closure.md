# Closure

此篇介紹一些關於`Closure`（閉包）的觀念

參考資料：[深入淺出了解JS閉包](https://pjchender.blogspot.com/2017/05/javascript-closure.html)

## Basic And Think：

* 當你看到一個_**Function**_ 裡面 `return` 另一個 _**Function**_，通常就是有用到閉包的概念。 
* 透過閉包，可以讓 _**Function**_ 有 `private` 變數。 
* 有點「為了解決不同函數，使用同一變數的問題」之概念。

## Example：

#### Basic Closure（基本示範）：

```javascript
function House(){
    var count =0;                //函式內要用到的變數
    function countAnimal(){        //真正要執行的函數
    count ++;
    console.log(count+'dogs');
    }
    return countAnimal            //執行完後把這個函式回傳出來
}
const FunctionName = House();   //有點拆封的感覺，這時的AAA會等於內部真正執行函數
FunctionName();                // 1 dogs 
//所以執行一次就會count++一次。而var count 只會做在 const AAA內行一次。         
```

#### More const（就算多個Function 使用同一個`House()`，也不會污染變數）：

```javascript
function House(){
    var count =0;                //函式內要用到的變數
    function countAnimal(){        //真正要執行的函數
    count ++;
    console.log(count+'dogs');
    }
    return countAnimal            //執行完後把這個函式回傳出來
}

const FunctionName1 = House();
const FunctionName2 = House();
const FunctionName3 = House();

FunctionName1();    //1 dogs
FunctionName1();    //2 dogs

FunctionName2();    //1 dogs
FunctionName3();    //1 dogs
```

#### 將參數帶入閉包中：

```javascript
function House(Animal) {
  var count = 0;                
  function countAnimal() {        
    count++;
    console.log(count +' '+Animal);
  }
  return countAnimal            
}

const FunctionName = House('Cat');        
FunctionName();  // 1 Cat
FunctionName();  // 2 Cat
FunctionName();  // 3 Cat

const FunctionName2 = House('Dog');        
FunctionName2();  // 1 Dog
FunctionName2();  // 2 Dog
FunctionName2();  // 3 Dog 
```

#### 簡潔寫法：

```javascript
function createCounter(name){
    var count=0
    //把此function 變成匿名函式
    return function(){
    count++;
    console.log(count + ' ' + name)
    }
}
const Animal1 = createCounter('Cat');
const Animal2 = createCounter('Dog');
const Animal3 = createCounter('Man');

Animal1();
Animal1();
Animal3();
Animal2();
```

## 範圍鏈：

* 內層 func 可以讀取外層的宣告變數，但外層的 func 讀不到內層宣告的變數。若是在自己層級找不到，就往外找，直到 Global為止。















