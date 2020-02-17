# Flyweight \(解释器模式\)

## Code

```javascript
let examCarNum = 0         // 驾考车总数
/* 驾考车对象 */
class ExamCar {
    constructor(carType) {
        examCarNum++
        this.carId = examCarNum
        this.carType = carType ? '手动档' : '自动档'
        this.usingState = false    // 是否正在使用
    }

    /* 在本车上考试 */
    examine(candidateId) {
        return new Promise((resolve => {
            this.usingState = true
            console.log(`考生- ${ candidateId } 开始在${ this.carType }驾考车- ${ this.carId } 上考试`)
            setTimeout(() => {
                this.usingState = false
                console.log(`%c考生- ${ candidateId } 在${ this.carType }驾考车- ${ this.carId } 上考试完毕`, 'color:#f40')
                resolve()                       // 0~2秒后考试完毕
            }, Math.random() * 2000)
        }))
    }
}

/* 手动档汽车对象池 */
ManualExamCarPool = {
    _pool: [],                  // 驾考车对象池
    _candidateQueue: [],        // 考生队列

    /* 注册考生 ID 列表 */
    registCandidates(candidateList) {
        candidateList.forEach(candidateId => this.registCandidate(candidateId))
    },

    /* 注册手动档考生 */
    registCandidate(candidateId) {
        const examCar = this.getManualExamCar()    // 找一个未被占用的手动档驾考车
        if (examCar) {
            examCar.examine(candidateId)           // 开始考试，考完了让队列中的下一个考生开始考试
              .then(() => {
                  const nextCandidateId = this._candidateQueue.length && this._candidateQueue.shift()
                  nextCandidateId && this.registCandidate(nextCandidateId)
              })
        } else this._candidateQueue.push(candidateId)
    },

    /* 注册手动档车 */
    initManualExamCar(manualExamCarNum) {
        for (let i = 1; i <= manualExamCarNum; i++) {
            this._pool.push(new ExamCar(true))
        }
    },

    /* 获取状态为未被占用的手动档车 */
    getManualExamCar() {
        return this._pool.find(car => !car.usingState)
    }
}

ManualExamCarPool.initManualExamCar(3)          // 一共有3个驾考车
ManualExamCarPool.registCandidates([1, 2, 3, 4, 5, 6, 7, 8, 9, 10])  // 10个考生来考试

```

## 解釋

* 運用共享技術有效地支持大量細節物件的複用。系統只使用少量的物件，而這些物件都很相似，狀態變化很小，可以實現對物件的多次複用。由於享元模式要求能夠共享的物件必須是較細節的物件，因此又稱為輕量級模式。

## 場景

* 文件上傳需要創建多個文件實體的時候 
* 如果一個應用程式使用了大量的物件，而這些大量的物件造成了很大的儲存開銷就應該考慮使用享元模式

## 優點

* 減少物件的創建，降低系統的內存，使效率提高

## 缺點

* 提升系統的複雜度，需要分離出外部狀態和內部狀態，而且外部狀態具有固有化的性質，不應該隨著內部狀態的變化而變化，否則會造成系統的混亂。



