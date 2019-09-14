# 基礎介紹

## 基礎

* MongoDB是資料庫的概念 
* 而在現今資料庫中又分成： 
  * SQL（關聯式資料庫） 
  * NoSQL（非關聯式資料庫）（此篇要講的）

## 思維

* Why NoSQL：面對巨量資料時，有著較佳的管理與分析 
* NoSQL與大數據的關係： 
  * 速度 
  * 多樣的資料格式：NoSQL屬於無綱要（Schemaless）設計，所以在儲存資料之前不需要事先定義資料庫綱要（你可以想像成不用先定義各種欄位） 
  * 資料量：處理大量資料

## NoSQL 分類

* 文件導向資料庫（Document）：MongoDB 
  * 應用場景：Web環境下的數據資料 
  * 說明：以集合方式儲存，每個集合（Collection）有多筆文件（Document）組成，每筆文件可為Web 結構化資料（如JSON） 
  * _**層級**_： 
    * 多個 Document，組成一個 Collection 。 
    * 多個 Collection，組成一個DB 
* 鍵值資料庫（Key-Value）：Redis、Dynamo 
  * 應用場景：內容快取 
* 列式資料庫（Column）：Cassandra、BigTable、Hbase 
  * 應用場景：分散式檔案系統 
* 圖形資料庫（Graph）：GraphDB 
  * 應用場景：社交網路 
  * 說明：採用圖結構的概念儲存資料，並利用圖結構相關演算法提高效能。











