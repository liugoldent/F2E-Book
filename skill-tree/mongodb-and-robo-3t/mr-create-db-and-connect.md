# Create DB & Connect DB

## Create DB

* 首先打開你的 Robo 3T。理論上，會出現一個如下的畫面

![](../../.gitbook/assets/create1.png)

* 按下 Create 會出現一個視窗，輸入一些資訊（通常自己學習我使用預設）

![](../../.gitbook/assets/create2.png)

* 填完，你可以按 Test 來測試，是否成功

![](../../.gitbook/assets/create3.png)

* 成功後，左方會出現一些資訊

![](../../.gitbook/assets/create4.png)

* 解釋上圖資訊 
  * 你連結到 New Connection 
  * 這個 Connection 內 有幾個資料庫（DB）：bac\_test、config、ntut、prodList（通常一開始應該為空的） 
  * 而每個資料庫中有都各有自己的集合（Collections）：prodList 
  * 各自的集合中，有各自的文件（Documents）：JSON data

## Connect DB

這邊我直接貼上，我連上DB的Code

如果連接成功、失敗、異常會出現哪些資訊。

```javascript
var mongoose = require('mongoose'),
  DB_URL = 'mongodb://localhost:27017/bac_test';//無密碼
/*
 * DB_URL 有密碼的話 
 * DB_URL = 'mongodb://abcd:12345@localhost:27017/bac_test';
 * abcd                是使用者帳號;
 * 12345               是使用者密碼;
 * localhost:27017     是連接網域;
 * bac_test            是資料庫名稱;
*/
 
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

//module.exports = mongoose;

```

















