# Express

## Introduction

* Express 是 Node.js 的開發框架 
* 可以用來開一個 Server 以及架一個 Router

## 實際應用

* 首先，你要先 `npm install express` 
* 再來，建立一個 `Route.js`

```javascript
var express = require('express');
var app = express();

app.listen(3000, function () {
  console.log('Example app listening on port 3000!');
});
//要先 listen 才會有localhost:3000這個 port

app.get('/',function(req,res){
res.send('input   [localhost:3000/get/All]   to get All Data')
});

app.get('/get/All', async function (req, ApiRes) {
  ApiRes.send('You get All Data')
//上面是單純 server 架好後
// localhost:3000/get/All 會得到一個 You get All Data
  
  try {
    var prodSchemaObj = require("./prodSchema.js");
    const DbRes = await prodSchemaObj.find({}).lean().sort({index: 1}).exec();
    ApiRes.json({ success: true, data: DbRes });
   }
   catch (e) {
     ApiRes.json({ success: false, message: e.message })
     console.error(e.stack);
   }
//try catch 部分為「想經由輸入某段 API 得到 Data」
});
```

* 最後輸入 `Node Route.js` 
* localhost:3000 服務成功

