# Webpack 打包工具
[img01]:/image/webpack.png "Webpack圖片"
![alt][img01]
## **一、如何使用Webpack**
### **1. 於專案資料夾內開啟終端機輸入npm init建立Node.js環境**
> 在資料夾啟用node.js服務，創建package.json文件。
```go
$npm init
```
### **2. 使用終端機安裝webpack**
> 安裝後產生node_modules資料夾，且package.json文件裡會出現webpack版本訊息。
```go
$npm install --save-dev webpack webpack-cli
或
$npm install -g webpack webpack-cli
```
### **3. (視需求創建dist及src資料夾)**
> dist放壓縮後的js檔案，src放原碼檔案。
### **4. 基本用法**
- ＊使用webpack壓縮檔案
```go
$webpack src/app.js dist/app.bundle.js
// src/app.js會壓縮檔案儲存至dist/app.bundle.js
```
- ＊使用webpack監聽檔案
```go
$webpack src/app.js dist/app.bundle.js --watch
// 當src/app.js檔案有更動時，會自動更改dist/app.bundle.js
```
## **如何使用Webpack配置文件**
> 可簡化Webpack的字元命令
### **1.創建webpack.config.js檔案**
### **2.開啟webpack.config.js修訂內容**
> webpack.config.js內的模組往後只需輸入webpack --watch等指令不須加上檔案名稱，即可工作。
```js
module.exports = {
    entry: './src/app.js', //輸入文件
    output: {
        filename: './dist/app.bundle.js', //輸出文件
        path: path.resolve(__dirname, './'),
    }
};

```
### **3.開啟package.json修訂內容**
> package.json裡的scripts可指定webpack 命令
- 設定watch取代"webpack --watch"
- 設定prod取代"webpack -p"
```go
{
  "name": "webpack-test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  //-------------------------------------------//
  "scripts": {
    "watch":"webpack --mode development --watch", //自動執行webpack(監聽)
    "start":"webpack --mode development", //development為不壓縮版本
    "deplay":"webpack --mode production", //production為壓縮版本
    "webpack": "webpack" //自動執行為壓縮版本
  },
  //-------------------------------------------//
```
便可在npm環境使用webpack指令
```go
$npm run watch
```
***
## **使用插建修改Html檔案**
> 整合修訂html文檔
```js
 plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
      tittle: 'webpack 練習',
      minify:{collapseWhitespace: true,}
      })
  ]
  //tittle 需再html 改為<tittle><%= htmlWebpackPlugin.options.title %></tittle>
```
***
## **使用loader處理Css.Sass**
### **1. 安裝css loader**
> 安裝後package.json會出現版本訊息
```go
$npm install --save-dev css-loader
$npm install --save-dev style-loader
```
### **2. 在webpack.config.js裡指定loader**
```go
module.exports = {
  module: {
    rules: [
      { test: /\.css$/, use: 'css-loader' },
      { test: /\.ts$/, use: 'ts-loader' }
    ]
  }
};
```
### **3. 在.css裡指定loader**
```go
import css from './app.css';
```
### **4. 安裝sass loader**
***
## **Babel轉換器使用**
> 其功能是將Vue.js文轉換成可讀js檔，或將ES6轉換為ES5
### **1. 安裝babel**
```go
$npm install --save-dev babel-loader
```
### **2.在webpack.config.js的rules裡指定loader**
```js
module: {
  rules: [
    { test: /\.js$/, exclude: /node_modules/, loader: "babel-loader" }
  ]
}
```
## [babel參考資料](https://www.babeljs.cn/docs/setup/#installation)
***
## **配置多個html文件**
***
## **如何將圖片打包**
### **1. 安裝 file-loader**
```go
$npm install --save-dev file-loader 
```
### **2.在webpack.config.js的rules裡指定loader**
```js
module: {
  rules: [
    {
        test: /\.(png|jpg|gif)$/,
        use: [
          {
            loader: 'file-loader',
            options: {}
          }
  ]
}