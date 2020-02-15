# Prototype（原型模式）

## Code 

```javascript
class Person {
  constructor(name) {
    this.name = name
  }
  getName() {
    return this.name
  }
}
class Student extends Person {
  constructor(name) {
    super(name)
  }
  sayHello() {
    console.log(`Hello， My name is ${this.name}`)
  }
}

let student = new Student("xiaoming")
student.sayHello()
//"Hello， My name is xiaoming"
```

## 意指

* 原型實例指像創建物件的種類，通過拷貝這些原型以達到創新新的物件
* 概念為創建一個共享的原型，通過拷貝這些原型來創建新的類。用於創建重複的物件，帶來性能上的提升

