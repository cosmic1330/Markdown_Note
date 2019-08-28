# **Html 第三天 | metadata 元件腳本標籤**
> - `<head>`
>    - `<meta>` 提供有關頁面的元信息
>    - `<title>` 設定文檔標題
>    - `<link>` 外部資源連接 支援 css文檔 圖檔 文字檔
>    - `<style>` 支援css樣式文檔
>    - `<base>` 指定url路徑
---
## `<head>`
> 對Html文檔的設定，提供瀏覽器了解該文檔 (head的內容不會出現在頁面上)
---
## `<title>`
> 對Html文檔添加標題
> - 你的搜尋排名title標籤佔了最重要的因素
> - `<title>`的重要性大於`<h1>`
---
## `<meta>`
> 設定該文檔的特性 (ex:編碼、文檔資訊、裝置螢幕設定)
 ### **屬性**
 1. name
 2. content

> * @為影響會SEO的標籤 
> - `<meta http-equiv="Content-Type" content="text/html; charset=utf-8">`  指定文檔的字符編碼
> - @`<meta name=”description” content=”網頁說明” />` 對
文檔的簡單描述
> - `<meta name="author" content="Chris Mills">` 作者資訊
> - `<meta name="generator" content="vscode">` 編輯器資訊
> - `<meta name="generator" content="Mozilla/3.0Gold(Win95)[Netscape]">` 編輯器資訊
> - `<meta name="viewport" content="width=device-width, initial-scale=1, maximum-scale=1">` 設定對行動裝置縮放
> - `<meta http-equiv="refresh" content="3;url=http://www.mozilla.org/">` 三秒後重置/導向網頁乙次
---
## `<link>`
> 定義文檔和外部資源之間的鏈接
 ### **屬性**
 1. rel 設定關係
  - stylesheet 樣式表
  - icon 網站圖標
  - apple-touch-icon-precomposed 移動平台圖標(要設size)
  - preload 表示瀏覽器應該預加載該資源
 2. href 指定被鏈接資源的URL
 3. type 包含了鏈接資源的MIME類型
 4. sizes 表示圖標大小
 5. media 設定加載的條件
 6. as 表示獲取特定的內容類( 該屬性僅在<link>元素設置了 rel="preload" 時才能使用 )
 7. integrity 用瀏覽器獲取的資源文件的hash值
 8. title 瀏覽器菜單 "查看>頁面樣式" 來選擇網頁的樣式。

```html
1. icon設定
<link rel="shortcut icon" href="favicon.ico" type="image/x-icon">
2. 多語言設定
<link rel="alternate" type="text/html" href="http://mysite.com/mypage-fr.htm" hreflang="en" title="French">
<link rel="alternate" type="text/html" href="http://mysite.com/mypage-jp.htm" hreflang="en" title="Japanese">
3. 多樣式設定
<link rel="stylesheet" type="text/css" href="http://mysite.com/style-regular.css" title="Regular Layout">
<link rel="stylesheet alternate" type="text/css" href="http://mysite.com/style-highcontrast.css" title="High Contrast Layout">

Read more: https://html.com/attributes/link-title/#ixzz5xdCbb8ES
```
---
## `<style>`
> 設定文檔的樣式
### **屬性**
1. type 該屬性以MIME類型
2. media 設定加載的條件
3. title 指定可選的樣式表
4. scoped 如果該屬性存在，則樣式應用於其**父元素**；如果不存在，則應用於整個文檔
```html
1.
<style type="text/css"></style>
2.
<style>
    @media (max-width: 600px) {
        .facet_sidebar {
            display: none;
        }
    }
</style>
3.
4.
<section>
    <style scoped>
      p { color: red; }
    </style>
    <p>This should be red.</p>
</section>
```