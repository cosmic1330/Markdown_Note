# Node.js
[npm說明](https://chriskang028.wordpress.com/2017/07/05/%E5%BC%84%E6%87%82-npm-install-%E7%9A%84-dependencies-v-s-devdependencies/)

## npm init
- 新專案創建新的npm資料夾
>如果有package.json 直接用npm install 即可下載套件

## -g 和 -d
>-g是下載到全域，-d是下載到資料夾內


## 一開始在使用 npm 管理安裝套件時，一定會對於這兩者很困惑：
- npm install packagename --save;
與
- npm install packagename --save-dev
![npmgd](/image/npmgd.png)
##  npm下載的檔案是從自身的資料庫
>因為無法確定來源，會有感染病毒風險

##node-webkit.js 視窗軟體設計 (nw.js)