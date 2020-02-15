# Chain of Responsibility \(職責鏈模式\)

## Code

```javascript
class Action {
    constructor(name) {
        this.name = name
        this.nextAction = null
    }
    setNextAction(action) {
        this.nextAction = action
    }
    handle() {
        console.log( `${this.name} 审批`)
        if (this.nextAction != null) {
            this.nextAction.handle()
        }
    }
}

let a1 = new Action("组长")
let a2 = new Action("经理")
let a3 = new Action("总监")
a1.setNextAction(a2)
a2.setNextAction(a3)
a1.handle()

//"组长 审批"
//"经理 审批"
//"总监 审批"
```

## 優點

* 降低耦合度。將請求者和接收者解偶
* 簡化了物件，使得物件不用知道鏈的結構
* 增強給物件指派職責的靈活性。通過改變鏈內的成員或者調動他們的次序，允許動態新增或刪除責任
* 增加新的請求處理方便

## 缺點

* 不能保證某個請求一定會被鏈中的節點處理，這種情況可以在鏈尾增加一個保底的接受者節點來處理這種即將離開鏈尾的請求
* 使程序中多了很多節點對象，可能在一次的請求過程中，大部分的節點並沒有實質的作用。他們的作用僅僅只是請求傳遞下去，從性能當面考慮，要避免過長的職責鏈到來的性能損耗

