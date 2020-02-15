# Bridge（橋接模式）

## Code

```javascript
class Color {
    constructor(name){
        this.name = name
    }
}
class Shape {
    constructor(name,color){
        this.name = name
        this.color = color 
    }
    draw(){
        console.log(`${this.color.name} ${this.name}`)
    }
}

//测试
let red = new Color('red')
let yellow = new Color('yellow')
let circle = new Shape('circle', red)
circle.draw()
//"red circle"
let triangle = new Shape('triangle', yellow)
triangle.draw()
//"yellow triangle"
```

## 優點

* 有助於獨立管理各組成成分，把抽象化實現解偶 
* 提高可擴充性

## 缺點

* 大量運用會導致開發成本增加。



