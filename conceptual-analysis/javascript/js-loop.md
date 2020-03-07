# Loop

## `for` 迴圈

#### 用於明確的迴圈執行次數

```javascript
var i;

for (i = 0; i < 10; i++) {
  // 做某件事
}
// i = 0 > 初始值
// i < 10 > 條件
// i ++ > 結束時i要做什麼事
```

## `while` 迴圈

#### （注意結束的條件要設好，否則會造成無窮迴圈）

#### 用於不明確的迴圈執行次數

```javascript
var i = 1; //初始值

while ( i <= 10 ){  // 條件
  console.log( i );
  i++; // 結束時 i 要做什麼事
}
```

## do while 迴圈

#### （注意結束的條件要設好，否則會造成無窮迴圈）

#### （建議先設定條件）

#### 用於不明確的迴圈執行次數

```javascript
var i =1; // 初始值
do{
  console.log(i)
  i++ // 結束時做啥
}while(i <= 10) // 條件
```

{% hint style="success" %}
#### break：直接跳離迴圈
{% endhint %}

{% hint style="success" %}
#### continue：會跳過一次，然後繼續下一次迴圈
{% endhint %}

#### 

