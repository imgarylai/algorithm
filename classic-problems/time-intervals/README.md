# Time Intervals 時間區間問題

LeetCode 有一系列的時間區間問題，這個題目是值得花時間投資的，因為題目的變形非常多，外加上現在公司的面試考題，已經不像是以往直接用 LeetCode 的原題，用很直觀的方式來描述題目，而是喜歡在題目上面加上自己公司產品的概念，讓大家更像在解決自家公司的實際問題，例如：如果是 Google ，很簡單的可以把題目變形成他們的行事曆 ，Amazon 可以是他們物流員工的排班時間，Airbnb 可以改變成客人的訂房時間區間，LinkedIn 可以問幫員工安排會議室，臉書可以問怎麼樣安排活動...等。超級容易套入到現實生活的例子。

時間區間可以考的點有：

1. 時間區間有沒有重複？
2. 時間區間如果有重複的話，要怎麼合併起來？
3. 時間區間會重複，那我們需要幾個會議室/幾個員工排班？
4. 插入一個時間區間，再問以上的所有問題
5. 給定好幾個員工的時間表，算出大家都有空的時間
6. 每次開會的時間都是固定的，給你所有時程的開始時間，計算出任何跟時間相關的題目
7. 時間區間如果都合併後，總共的花費時間是多少？
8. 給出兩個人的時間表，找出他們哪些時間是同時在工作的
9. 找出重複的時間區間，盡可能地找到最多的非重疊時間區間，有哪些時間區間？要刪除幾個時間區間？
10. ...等各種變形

時間區間的問題最重要的就是兩兩區間之間的關係，大多數的題目就是去比較當前區間與**前一個區間**的重疊性。

