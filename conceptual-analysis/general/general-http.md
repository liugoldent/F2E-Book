# HTTP

## Cookie、LocalStorage、SessionStorage的差異

資料來源：[Charlie Chen on Medium](https://medium.com/@jscinin/javascript-cookie-localstorage-sessionstorage-%E4%B8%89%E7%A8%AE%E5%B7%AE%E7%95%B0-fe7f38260439)

| 特性 | Cookie | LocalStorage | SessionStorage |
| :--- | :--- | :--- | :--- |
| 數據的生命週期 | 由服務器生成，可設置失效時間。如果在瀏覽器端生成Cookie，默認是關閉瀏覽器後失效。 | 除非被清除，否則永久保存。 | 僅在當前有效，入關閉頁面或瀏覽器後被清除。 |
| 存放數據的大小 | 4 KB 左右 | 5 MB | 同左 |
| 與服務器端的通性 | 攜帶於HTTP 中，如果使用Cookie 保存過多數據，會導致性能問題。 | 僅在客戶端（Web）中保存，不參與和服務器的通信。 | 同左 |
| 易用性 | 需要程序員自行封裝，原生的Cookie 接口並不好。 | 原生接口可以接受，亦可再次封裝來對物件和陣列有更好的支持。 | 同左 |



