# **Html 重點整理**
![HTMLXMind](/image/Html.png)
## **`語意標籤`**
> 提供瀏覽器更容易導讀

![語意標籤](/image/website_html5_area-1.png)
### - **`Header`**
### - **`nav`**
### - **`main`**
> 每個頁面中只能有一個`<main>`標籤
### - **`aside`**
### - **`footer`**
### - **`標題集合標籤`**
- `<hgroup>`
> 當內容有主標題及次標題等⋯⋯多個標題的狀況下使用。
```go
<article>
<hgroup>
<h2>sub title</h2>
<h1>Main Title</h1>(主標題)
</hgroup>
</article>
```
### - **`圖片專用標籤`**
- `<figure><figcaption>`
> 先用`<figure>`來包覆圖片區塊，再使用`<figcation>`來描述此張圖片的標題。
```go
<figure>
    <img src="" alt="">
    <figcaption>
        <h3>標題</h3>
        <p>內容</p>
    </figcaption>
</figure>
```
### - **`<time>`**
> 用來標記時間
```go
<p>我在 <time datetime="2018-08-08">父親節</time> 有個家庭聚餐。</p>
``` 
### - **`<small>`** 
> 版權資訊或免責聲明, 注意事項等一些”附屬細則” 資訊, 如是整篇都為法律資訊的頁面則不須用small區隔。
### - **`<mark>`** 
> 如黃色螢光筆的方式畫出重點
### - **`<em>`** 
> 類似mark, 但這是真正文中需要強調的部分, 而mark只是意在凸顯某區塊
### - **`<strong>`** 
> 類似em, 但是通常用來包極重要的某句話或段落, em則是包某個詞`<b>` 關鍵字或產品名
### - **`<cite>`** 
> 標籤通常表示它所包含的文本對某個參考文獻的引用，比如書籍或者雜誌的標題。按照慣例，引用的文本將以斜體顯示。
### - **`<addressrk>`** 
> 應用於標記目前`<article>`或文件作者的聯絡資訊, 而不是作為一般標記地址用
***
## **`Table標籤`**
```go
<table>
  <caption>資料</caption>
  <thead>
    <tr>
      <th>Month</th>
      <th>Savings</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <td>January</td>
      <td>$100</td>
    </tr>
  </tbody>
  <tfoot>
    <tr>
      <td>總共</td>
      <td>$100</td>
    </tr>
  </tfoot>
</table>
```
### - **`<thead>`**
> 語意標籤，用來包覆標題的th
### - **`<tbody>`**
> 語意標籤，用來包覆內容的td
### - **`<tfoot>`**
> 語意標籤，用來包覆結尾的td
### - **`<td>`**
> 表格中的 **`行`**
### - **`<th>`**
> 表格中標題的 **`行`**
### - **`<tr>`**
> 表格中的 **`列`**
### - **`<rowspan>`**
> 合並儲存格的列
### - **`<colspan>`**
> 合並儲存格的行
### - **`<caption>`**
> table的標題
***
## **`Form標籤`**
### - **`<input>`**
> 輸入的type共有下列： 可搭配output顯示
- button、checkbox、color、date
- datetime-local、email、file、hidden
- image、month、number、password
- radio、range、reset、search
- submit、tel、text、time、url、week
```go
<form oninput="x.value=parseInt(a.value)+parseInt(b.value)">0
  <input type="range" id="a" value="50">100
  +<input type="number" id="b" value="50">
  =<output name="x" for="a b"></output>
</form>
```
### - **`<textarea>`**
> 可設定屬性 rows="4" cols="50" maxlength="200"
### - **`<button>`**
> 按鈕標籤
### - **`<select>`**
> 下拉式選單標籤
### - **`<label>`**
> 將表單控件作聯繫，為標記標籤的內容(點擊內容就能觸發input等控鍵)
```go
<label for="male">Male</label>
<input type="radio" name="sex" id="male" />
//隱式連繫
<label>Male
<input type="radio" name="sex" />
</label>
//顯示連繫
```
## Preload & Prefetch
>對於當前頁面很有必要的資源使用 preload，對於可能在將來的頁面中使用的資源使用 prefetch