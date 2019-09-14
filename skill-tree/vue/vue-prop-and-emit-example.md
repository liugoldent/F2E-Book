# Prop And Emit

## Conceptual

* 每個Vue實例中，實現事件接口 
  * 使用`$on(eventName）`監聽事件 
  * 使用`$emit(eventName , optionalPayload）`觸發事件

## Prop Code

參考資料：

* [CSDN：vue中關於$emit的用法](https://blog.csdn.net/sllailcp/article/details/78595077)

### Parent

```javascript
<template>
    <div>
        <div>父组件的toCity{{toCity}}</div>
        <train-city @showCityName="updateCity" :sendData="toCity"></train-city>
    </div>
<template>

<script>
  import TrainCity from "./train-city";
  export default {
    name:'index',
    components: {TrainCity},
    data () {
      return {
        toCity:"北京"
      }
    },
    methods:{
      updateCity(data){//触发子组件城市选择-选择城市的事件
        this.toCity = data.cityname;//改变了父组件的值
        console.log('toCity:'+this.toCity)
      }
    }
  }
</script>
```

### Child

```javascript
<template>
  <div class="train-city">
    <h3>父组件传给子组件的toCity:{{sendData}}</h3> 
    <br/><button @click='select(`大连`)'>点击此处将‘大连’发射给父组件</button>
  </div>
</template>

<script>
  export default {
    name:'trainCity',
    props:['sendData'], // 用来接收父组件传给子组件的数据
    methods:{
      select(val) {
        let data = {
          cityname: val
        };
        this.$emit('showCityName',data);//select事件触发后，自动触发showCityName事件
      }
    }
  }
</script>
```

### 流程說明：

1. 父組件在渲染畫面時，遇到 `train-city`組件，就去子組件找`template` 渲染出來 
2. 子組件遇到`sendData`就到`props:['sendData']`中找尋資料， 
3. 發現是`props`就去父組件找 `:sendData` 
4. 然後發現父組件中設定的，`:sendData =" toCity"` （綁定） 
5. 所以子組件的這個 `sendData` 就會等於 `toCiry` 的值。

## Emit Code

參考資料：

* [CSDN：關於vue.js中this.$emit的理解](https://blog.csdn.net/qq_34129336/article/details/79546077)

### Parent

```javascript
<template>
   <div>
     <p> {{ total }} </p>
     
     <my-button4 @increment1= "incrementTotal1" ></my-button4>      
     <!--自定義方法increment1監聽子組件觸發情況-- >
 
     <my-button4 @increment2= "incrementTotal2" ></my-button4>      
     <!--自定義方法increment2監聽子組件觸發情況-->
 
    </div>
    
 </template>
 <script>
 import myButton4 from '. /components/myButton4.vue'
 export default {
     data (){
       return {
           total : 0
       }           
     } ,
     methods :{
       incrementTotal1 : function () {  /*事件incrementTotal觸發*/
       this . total += 1
       } ,
       incrementTotal2 : function () {  /*事件incrementTota2觸發*/
       this . total += 2
       }                                      
     } ,
     components :{ /*子組件的實例，要盡量放在最後，不然會出現一些不必要的問題*/
     myButton4          
    }
}
</script>
```

### Child（myButton4.vue）

```javascript
<template>
       <button @click= "incrementCounter" > {{counter}} </button> 
       <!--在子組件中創建一個按鈕，創建點擊事件-->
</template>

<script>
 export default {
    data (){
        return {
          counter : 0
        }    
    },
    methods : {
        incrementCounter : function (){
          this . counter += 1
          this .$emit( 'increment1' )         
          /*觸發自定義事件increment1，也就是父組件中的incrementTotal1事件*/
          this .$emit( ' increment2' )         
          /*觸發自定義事件increment2，也就是父組件中的incrementTotal2事件*/
          /*這兩個事件一次只會觸發一個，為什麼呢？很簡單，因為每次只單擊一個按鈕*/
         }                              
     }
   }
</script>
```

### 流程說明：

1. 在父組件渲染畫面時，會渲染出_**一個數值**_，與_**兩個按鈕（子組件）**_ 
2. 當觸發第一個按鈕時（`@increment1="incrementTotal1"`），會到子組件找出_`@click="incrementCounter"`_ 
3. 你可以把子組件想成 `@increment1 = "incrementCounter"` 
4. 子組件就會通知它的 `methods：incrementCounter`要動作囉 
5. 而子組件，就會_**emit（發送）**_消息，跟父組件說 `incrementTotal1`要動作了 
6. 這時父組件，就會去通知它的`methods：incrementTotal1`動作。

## 















