# **HTML 第一天 | 主結構是什麼**
今天來說說HTML的主要結構，共分為四大區塊
1. DOCTYPE html
2. html 
3. head
4. body

---
## DOCTYPE
`定義該文檔是使用哪個版本的HTML或XML`

* HTML5
```js
<!DOCTYPE html>
```

* HTML4.01
```js
//嚴格模式
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01//EN" "http://www.w3.org/TR/html4/strict.dtd">
//Transitional模式
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Transitional//EN" "http://www.w3.org/TR/html4/loose.dtd">
//框架集模式
<!DOCTYPE HTML PUBLIC "-//W3C//DTD HTML 4.01 Frameset//EN" "http://www.w3.org/TR/html4/frameset.dtd">
```

* XML1.0
```js
//嚴格模式
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Strict//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-strict.dtd">
//Transitional模式
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Transitional//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-transitional.dtd">
//框架集模式
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.0 Frameset//EN" "http://www.w3.org/TR/xhtml1/DTD/xhtml1-frameset.dtd">
```

* XML1.1
```js
<!DOCTYPE html PUBLIC "-//W3C//DTD XHTML 1.1//EN" "http://www.w3.org/TR/xhtml11/DTD/xhtml11.dtd">
```
---
## \<html> Html Tag
`為主要根元素，文檔內容由此包覆。`
其中標籤元素又分為
+ metadata 元件腳本標籤
+ Sectioning root  根章節標籤
+ Content sectioning 內容語意標籤
  + Text content 區塊標籤
  + Inline text semantics 行內標籤
    + Image and multimedia 影音標籤
    + Demarcating edits 標記標籤
    + Forms 表單標籤
  + Table content 表格標籤
  + Embedded content 外嵌標籤
  + Web Components 模組標籤
+ Scripting JavaScript標籤
---

> ## **metadata 元件腳本標籤**
> - `<head>`
>    - `<meta>` 提供有關頁面的元信息
>    - `<title>` 設定文檔標題
>    - `<link>` 外部資源連接 支援 css文檔 圖檔 文字檔
>    - `<style>` 支援css樣式文檔
>    - `<base>` 指定url路徑

---

> ## **Sectioning root 根章節標籤**
> - `<body>`

---

> ## **Content sectioning 內容語意標籤**
>> 提供瀏覽器更容易導讀
> - `<header>`
>     - `<h1>`
>   - `<nav>`
> - `<main>` ＊每個頁面只能擁有一個main
>   - `<article>`
>     - `<address>` 聯絡訊息標籤
>   - `<section>`
>   - `<figure>` 圖片專用標籤
>     - `<figcation>` 用來描述此張圖片的標題。
>   - `<hgroup>` 主副標群組標籤
>     - `<h2>`,`<h3>`,`<h4>`,`<h5>`,`<h6>`
> - `<aside>`
> - `<footer>`

---

> ## **Scripting JavaScript標籤**
> - `<canvas>`
> - `<script>`


我先從SEO開始吧，
下一章節我們將詳細來介紹
**什麼是語意標籤**



參考文件
 [w3schools](https://www.w3schools.com/tags/tag_doctype.asp)
 [MDN](https://www.w3schools.com/tags/tag_doctype.asp)