# Javascript的基本觀念
[img01]:/image/js.png "JS圖片"
![alt][img01]
## **一、立即函式** IIFE

```js
(function(){
  Hellow word
})(); 
```
將立即函示包在程式外層，可避免程式內的全域變數遭外域變數取代。
***
## **二、嚴格模式 strict mode** 
```go
"use strict";
//將它加在函式內
```
透過strict mode來限制一些比較鬆散的寫法跟可能發生問題的地方，例如:避免原生JS的hoisting造成的宣告與使用問題。

`優點`

- 可以撰寫出嚴謹的JS
- 避免物件和變數定義重複的名稱

`缺點`

- Browser( 瀏覽器 ) 支援程度需要先確認

| 瀏覽器名稱 | 版本 |
|-----------|------|
| IE        |10、11|
| Chrome    |13 -  |
| Edge      |12 -  |
| Firefox   |4-62  |
| Safari    |6 -   |

***

## **三、變數** 
### **什麼時候應該使用變數**
1. 常常使用的時候
2. 客戶需要常常修改
### **變數種類**
1. 全域變數 
2. 區域變數

### `全域變數 Global Variable`
> 在函式之外 所宣告的變數就是全域變數，其值可在整個程式中存取和修改。
```js
var abc="hello"
function(){
    console.log(abc);
    //值為 hellow
}
```
在瀏覽器下的全域物件是 window，有以下方式所產生的變數都會在 window 內。
- 已宣告的變數是全域物件裡的一個無法變更 (non-configurable) 的屬性, 而未宣告的變數則是可變更的。

- 如果使用 var 則會先在記憶體準備一個空間給他，所以執行以前使用這個變數還不至於跳錯，但如果沒有使用 var，則會跳出錯誤。
```js
console.log(mom); // undefined
var mom = '老媽';

console.log(mom); // undefined
var mom = '老媽';
```
### `區域變數 Local Variable`
> 在函式中宣告的變數，每個函式間的區域變數互不干涉，也無法在函式外其他地方調用。
```JS
function(){
  var bcd = 'Hellow world';
  console.log(bcd);
  //值為Hellow world
}
```
### 變數宣告
* ### Var
1. 可重複定義，但會造成產生bug 
2. 會自動hoisting， 故推薦使用let const養成先宣告後使用的習慣
* ### let
1. ES6變數宣告，在區域變數時使用
* ### const
2. ES6變數宣告，在常數時使用

※ 注意 !! undefined表示 有發現變數但沒有值  not defined表示沒有發現變數。
***
## **四、函式  funciton**

### 注意
- 如果沒有return，會回傳undefined的值
- 需要控制執行時間時，使用function，反則js依照行數執行。
- return false時，則funtion中斷(假如return之後還有code也不會執行)

### `箭頭函式 Arrow function`
- 箭頭函式裡不會擁有自己的this
- 單行陳述不需要{}，且可以不寫return
- 只有一個參數可以不加()
- 沒有參數時一定要有()
```JS
正常寫法：
var callSomeone = (someone) => {
  return someone + '吃飯了'
}

省略寫法(單行、沒有參數時) :
var callSomeone = () => '小明' + '吃飯了' 

```
## **五、判斷式  Judgment**
`If判斷式有三種寫法`
1. 第一種寫法
> 正常寫法 使用if
```JS
if (this.dataset.sizing) {sizing = "true";}
```
2. 第二種寫法
> 使用三元運算式來判斷
```JS
sizing = this.dataset.sizing ? "true" : "false";
```
3. 第三種寫法
> 使用 || 來判斷
```JS
sizing = this.dataset.sizing || '';
```
`Switch的使用方式`
> 當有多條件匹配時使用
```JS
week = 3;
  console.log(week);
  switch(week){
      case 1:
      console.log("今天星期一");
      break;

      case 2:
      console.log("今天星期三");
      break;

      case 3:
      console.log("今天星期三");
      break;

      default:
      console.log("今天禮拜?");

  }
```
## **六、陣列及物件**
> 物件與陣列皆使用在紀錄資料
* 物件及陣列"傳址傳值"時會被取代，其他的變數則不會。
```JS
物件管理"同屬"的資料
let jeff ={
	name:"jeff",
	sex:"male",
	bold:"B"};
陣列管理"同類"的資料
let peoples =[
       "alex",
       "jeff",
       "sara"];
```
### `物件的管理方法`
> 使用 Array.map、Object.values 和 Object.keys 處理「物件中有物件」和「陣列中有物件」的情況。

以下為一個物件範例
```js
var rex = {
    name:'jeff',
    writeName:function(){
      return 'Name is ' + this.name;},
    id:1
};
```
- Object.keys
```js
Object.keys(rex); //使用Object.keys會索取物件內的Key，並回傳成一個陣列
//["name","writeName","id"]
```
- Object.value
```js
console.log(rex.name); //會取得'jeff'
console.log(rex.writeName); //會取得一個函式內容
rex.age=20; //新增一個age的key和值
console.log(rex.age); //會取得20
```
### `陣列的管理方法`
- 取值
```js
let peoples =["alex","jeff","sara"];
peoples[1]; //"jeff"
```
- 增加

```js
let peoples =["alex","jeff","sara"];
peoples.push("mary"); //["alex","jeff","sara","mary"]
```
- 提取並刪除最後一個
 
```js
let peoples =["alex","jeff","sara"];
peoples.pop(); //從陣列中踢除並取出最後一個 "mary"
```
- 提取並刪除第一個
 
```js
let peoples =["alex","jeff","sara"];
peoples.shift(); //從陣列中踢除並取出第一個 "alex"
```
- 在陣列中首位新增
 
```js
let peoples =["alex","jeff","sara"];
peoples.unshift("mary") //從陣列中第一位塞入資料 //["mary","alex","jeff","sara"]
```
### `進階陣列處理方法`
#### 1. filter
> 生成一個陣列，其條件符合 return 後方為 true 的物件，很適合用在搜尋符合條件的資料。
```js
var a = [1,2,3,4];
var newa = a.filter(function(x){
 return x > 1;
});
console.log(newa,a); 
//newa : 2 3 4    //a: 1 2 3 4
```
#### 2. map
- 如果不回傳則是 undefined
- 回傳數量等於原始陣列的長度

> 適合將原始的變數運算後重新組合一個新的陣列。

```js
var a = [1,2,3,4];
var newa = a.map(function(x){
 return x = x+1;
});
console.log(newa,a); 
//newa : 2 3 4 5   //a: 1 2 3 4
```
#### 3. forEach
- 不會產生新的陣列
> 單純執行每個陣列內的物件或值
```js
var a = [1,2,3,4];
var newa = a.forEach(function(x){
 console.log(x);
});
console.log(newa,a);  
//1
//2
//3
//4
//undifined  //1 2 3 4 
```
#### 4. reduce
>  接受一個函數作為累加，依序加上下一個值。
```js
var a = [1,2,3,4];
var new = a.reduce(function(total, current){
 return total + current;
},100);
console.log(new,a);
//10   //1 2 3 4
``` 
[陣列參考資料](https://wcc723.github.io/javascript/2017/06/29/es6-native-array/)
## **七、Console的除錯應用**
- console.log() 顯示值
- console.table() 表格顯示資料
- console.time() 計時開始
- console.timeEnd() 計時結束
- devtool的除了console及Elements常使用，Sources可設定斷點 及監聽事件  Watch可監看參數
## _`N、this的重要觀念`_
this永遠指向最後調用它的對象

1. 純粹的調用
  > this會指向window
```JS
var name = '全域';
function callMethod() {
  var name = '區域'
  console.log(this.name)
  return function () {    // << 閉包
    var name = '區域的內層變數';
    console.log(this.name)
  }
}
callMethod()();//執行callMethod、callMethod裡的函式
//值為全域 全域
```
2. 物件的方法調用
  - Object
3. DOM 物件調用 
  - Object
4. 建構式的調用
  - Object  > 屬於 new 它的物件
5. bind, apply, call
  - 傳入的物件
6. 箭頭函示 >箭頭函數會自動將 this 變數綁定到其定義時所在的物件
  - window 或 定義的環境
# _尚未完成_
***
