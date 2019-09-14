# CRUD in Robo 3T

## 定義

* C：Create（新增） 
* R：Read（讀取） 
* U：Update（更新） 
* D：Delete（刪除）

## 預先準備：

* 聲明：以下檔案都_**設定在同一層中**_ 
* 一開始一定要先 `npm install mongoose` 
* 首先準備 `db.js`。_**目的是連接 db**_

```javascript
// db.js
var mongoose = require('mongoose'),
  DB_URL = 'mongodb://localhost:27017/bac_test';
/* *
 * 連接
 */
mongoose.connect(DB_URL);

/* *
  * 連接成功
  */
mongoose.connection.on('connected', function () {
  console.log('Mongoose connection open to ' + DB_URL);
});

/* *
 * 連接異常
 */
mongoose.connection.on('error', function (err) {
  console.log('Mongoose connection error: ' + err);
});

/* *
 * 連接斷開
 */
mongoose.connection.on('disconnected', function () {
  console.log('Mongoose connection disconnected');
});

module.exports = mongoose;
```

* 再來準備 `prodSchema.js`。_**目的是制定輸入資料格式**_。

```javascript
var mongoose = require('./db.js')
//把 db require 進來
var prodSchema  = mongoose.Schema({       
    name :{ type: String },       
    display_name_en : { type: String },       
    display_name_zh_TW : { type: String },       
    sort:{type:Number},
});
module.exports = mongoose.model('prodSchema',prodSchema,'prodList');
//第一個prodSchema代表，輸出東西叫做prodSchema
//第二個prodSchema代表，輸出格式為prodSchema
//最後面的prodList代表連接到那個DB
```

## CRUD

### 「C」

```javascript
//Create.js
var prodSchema = require("./prodSchema.js");

function InsertNew(){
    
    let prodSchemaArray = new prodSchema({
      "name": "Keedem",
      "display_name_en": "Kuan",
      "display_name_zh_TW": "冠",
      "sort": 1
    });

    prodSchemaArray.save(function (err, res) {
      console.log("res",res)
      err?console.log("Error:" + err):console.log("ok")
    });
  }
  InsertNew()
```

`node Create.js` 動作



### 「R」

```javascript
//Read.js
var prodSchemaArray = require("./prodSchema.js");
prodSchemaArray.find({}, (err, res) => {
//這邊的 find{}，可以塞條件進去
    if (err) {
      return console.error(err);
    }
    var WantResult = res;
    console.log(WantResult);
  });
```

`node Read.js` 動作



### 「U」

```javascript
//Update.js
var prodSchemaArray = require("./prodSchema.js");

/**
 * @parum multi:true 為修改多筆
 */
prodSchemaArray.update(
    { display_name_en: "Kuan" }, //舊有資料
    { display_name_en: "Guan"},  //更新資料
    { multi: false}, 
    function(err, docs){
    if(err) console.log(err);
    console.log('更改成功：' +docs);
    })
```

`node Update.js` 動作



### 「D」

```javascript
//Delete.js
var prodSchemaArray = require("./prodSchema.js");
/**
 * deleteOne 為刪除一筆
 * deleteMany 為刪除多筆
*/
prodSchemaArray.deleteOne(
   { display_name_en: 'Guan' }, 
   function (err) {});
//or
//prodSchemaArray.deleteMany({ imageType: 'technics' }, function (err) {})
```

`node Delete.js` 動作











