# Composite（組合模式）

## Code

```javascript
class TrainOrder {
	create () {
		console.log('创建火车票订单')
	}
}
class HotelOrder {
	create () {
		console.log('创建酒店订单')
	}
}

class TotalOrder {
	constructor () {
		this.orderList = []
	}
	addOrder (order) {
		this.orderList.push(order)
		return this
	}
	create () {
		this.orderList.forEach(item => {
			item.create()
		})
		return this
	}
}
// 可以在购票网站买车票同时也订房间
let train = new TrainOrder()
let hotel = new HotelOrder()
let total = new TotalOrder()
total.addOrder(train).addOrder(hotel).create()

//"创建火车票订单"
//"创建酒店订单"
```

## 優點

* 將物件組合成樹狀結構，以表示整體部份的層次結構
* 通過物件的多型表現，使得用戶對單個物件或組合物件使用具有一致性

## 場景

* 表示物件-整體層次結構
* 希望用戶忽略組合物件和單個物件的不同，用戶將統一的使用組合結構中的所有物件

## 缺點

* 通過組合模式創建太多物件，會造成維護的負擔

