# Command \(命令模式\)

## Code

```javascript
// 接收者类
class Receiver {
    execute() {
      console.log('接收者执行请求')
    }
  }
  
// 命令者
class Command {  
    constructor(receiver) {
        this.receiver = receiver
    }
    execute () {    
        console.log('命令');
        this.receiver.execute()
    }
}
// 触发者
class Invoker {   
    constructor(command) {
        this.command = command
    }
    invoke() {   
        console.log('开始')
        this.command.execute()
    }
}
  
// 仓库
const warehouse = new Receiver();   
// 订单    
const order = new Command(warehouse);  
// 客户
const client = new Invoker(order);      
client.invoke()

```

##  優點

* 對命令進行封裝，使命令易於擴展和修改 
* 命令發出者和接受者解耦，使發出者不需要知道命令的具體執行過程即可執行

## 缺點

* 使用命令模式可能會導致某些系統有過多的具體命令類

