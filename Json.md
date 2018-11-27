# JSON的基本觀念
[imag01]:/image/json.png "JSON圖片"
![alt][imag01]
## **何謂JSON**
> 物件中的陣列，由文字格式組成

`儲存時`
### JSON需將物件轉換為字串儲存
```js
let point={"x":3, "y":4}; // 這是物件
   let jsonStr=JSON.stringify(point); // 轉換成字串 */
```
`提取時`
### 可將JSON轉換為物件
```js
 let jsonStr="{\"n1\":3, \"n2\":4}"; // 這是字串
   let point=JSON.parse(jsonStr); // 轉換成物件 */
```
## ※注意
- 假如資料是與server處理 則需要加入延遲時間
- 假如是從外部撈回的資料 要先做字串處理 不可直接使用innerHTML(有安全疑慮)
