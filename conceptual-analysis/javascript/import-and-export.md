# Import And Export

以下會介紹常用到的 Import And Export

* In _**ES5**_：Use `require` 
* In _**ES6**_：Use `import` （Notice You Need Use _**Babel**_ to Compile）

參考資料：[只是個打字的-淺談JS Import and  Export](https://blog.typeart.cc/%E6%B7%BA%E8%AB%87JavaScript%20ES6%E7%9A%84import%E8%88%87import%7B%7D%E5%8F%8Aexport%E5%8F%8Aexport%20default%E4%BD%BF%E7%94%A8%E6%96%B9%E5%BC%8F/)

## Export vs Export default

* 差別在於一個檔案內，Export 可以有無限多個，但Export Default 只能有一個。 
* 並且在使用_**Default**_ 時，要把`Export`的東西寫進一個`{}`內。

```javascript
export const a=123;
export const myFunc =()=>{console.log('this is myFunc'}

//So，以上顯示可以輸出很多Export

//So，以下顯示只能輸出一個Export Default
const test=()=>{'this is test'}
export default()=>{
    b:'b',
        test
}
```

* 如果是 _**無Default**_ 的`Export`

首先`export`的js檔寫成如下

```javascript
//module "my-module.js"
export { cube, foo, graph}
```

另一個`import`的JS檔則要寫成

```javascript
import {cube,foo,graph} from 'my-module'
```

* 如果是 _**Default**_ 的 `Export`

```javascript
//module 'my-module2.js'
export default function cube(x){
return x*x*x
}
```

另一個`import`的JS則寫成

```javascript
import cube from 'my-module2';
console.log(cube(3)); //27
```

* 總結是`Default` 輸出後，在`Import` 時不用`{}`括號。

{% hint style="info" %}
注意：預設輸出`（Export Default）`不得使用 `var / let / const`

口訣：有 _**Default**_ 了，_**不用**_ 特地去_**括號引入**_。
{% endhint %}

## Import vs Import { }

* 總結：最基本的為，`Export` _**有Default**_，就不用 `{}`

以下介紹一些常見使用 Import 的方式

（定義模塊：所謂的模塊，就是你所「Export檔案」的「那個Export」稱作模塊）

1. 引入整個模塊的內容   


   ```javascript
   import * as myModule from '/modules/my-module.js';
   //my-module.js 就是你的Export檔案（又稱作模塊文件）
   //然後你可以對myModule施加方法
   myModule.filter();
   ```

2. 從模塊文件引入，但單一輸出  


   ```javascript
   import {myExport} from '/modules/my-module.js';
   ```

3. 從模塊文件引入，但多輸出  


   ```javascript
   import {foo,bar} from '/modules/my-module.js';
   ```

4. 重命名輸出的模塊（重命名單一模塊）（稱作_**alias**_）  


   ```javascript
   import {foo as shotName} from '/modules/my-module.js';
   ```

5. 重命名多個輸出模塊（稱作 _**aliases**_）  


   ```javascript
   import {foo as shotName,
           bar as short
   } from '/modules/my-module.js';
   ```

6. 僅作為 _**Side Effect**_ 引入模塊文件（模塊文件不做動作，而是執行整塊模塊文件的程式）  


   ```javascript
   import '/modules/my-module.js';
   ```

7. 預設使用  


   ```javascript
   import myDefault,{foo,bar} from '/modules/my-module.js';
   ```

8. 動態引入  


   ```javascript
   import ('/modules/my-module.js')
       .then((module)=>{
       //做點事情
       });
   ```

   ```javascript
   let module = await import('/modules/my-module.js');
   ```

  









