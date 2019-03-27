# Webpack 打包工具
[img01]:/image/webpack.png "Webpack圖片"
![alt][img01]
## **`安裝Webpack`**
### **1. 於專案資料夾內開啟終端機輸入npm init建立Node.js環境**
> 在資料夾啟用node.js服務，創建package.json文件。
```go
$npm init
$npm install
$npm run watch
```
### **2. 使用終端機安裝webpack**
> 安裝後產生node_modules資料夾，且package.json文件裡會出現webpack版本訊息。
```go
$npm install --save-dev webpack webpack-cli
或
$npm install -g webpack webpack-cli
```
- 安裝完成後會再package.json中的"devDependencies"出現版本訊息
### **3. 新增webpack.config.js檔案**
> 此檔案為設定Webpack的設定檔，輸入及輸出路徑和壓縮都在此檔設定完成。
### **4. 設定package.json的script**
> 設定script可以使指令更簡潔，設定後便可在終端機使用npm run watch執行webpack指令

```go
{
  "name": "webpack-test",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  //-------------------------------------------//
  "scripts": {
    "watch":"webpack --mode development --watch", 
    //自動執行webpack(監聽)
    "start":"webpack --mode development", 
    //development為不壓縮版本
    "deplay":"webpack --mode production", 
    //production為壓縮版本
    "webpack": "webpack" //自動執行為壓縮版本
    "dev": "webpack-dev-server --inline --hot"
    //webpack-server開啟
  },
  //-------------------------------------------//
```
> npm run watch;
npm run dev;
npm run start;
### **5. 設定好就可以開始壓縮囉**
- 使用webpack壓縮檔案`(如果未設定--mode development都會自動文字壓縮)`
```go
$webpack src/app.js dist/app.bundle.js
// src/app.js會壓縮檔案儲存至dist/app.bundle.js
```
- 使用webpack監聽檔案
```go
$webpack src/app.js dist/app.bundle.js --watch
// 當src/app.js檔案有更動時，會自動更改dist/app.bundle.js
```
***
## **`如何設定webpack.config.js`**
webpack.config.js的結構分為
- entry
- output
- module
- plugins
- resolve

`基本結構圖`
```js
module.exports = {
  entry: './src/app.js', //輸入文件
    output: {
        filename: '[name].bundle.js', //輸出文件
        path: path.resolve(__dirname, 'dist'), //resolve 相對路徑轉絕對路徑
    },
  module: {
    rules: [
      {
        test: /\.m?js$/,
        exclude: /(node_modules|bower_components)/,
        use: {
          loader: 'babel-loader',
          options: {
            presets: ['@babel/preset-env'],
            plugins: ['@babel/plugin-proposal-object-rest-spread']
          }
        }
      },
      
    ]
  },
  resolve: {
    extensions: ['.wasm', '.mjs', '.js', '.json']
  }
};

```

## **`mode`**
> 告知 webpack 使用相應模式的內置優化，有以下兩種模式
- --development 不壓縮字形版本
- --production 壓縮字形版本
```go
module.exports = {
  mode: 'production'
};
//也可在npm 執行時設定(＊ 請看上方資料 )
```
## **`entry`**
> 起點或是應用程序的起點入口。從這個起點開始，應用程序啟動執行。如果傳遞一個數組，那麼數組的每一項都會執行
```go
module.exports = {
  entry: {
    home: './home.js',
    about: './about.js',
    contact: './contact.js'
  }
 /*每個 HTML 頁面都有一個入口起點。
   單頁應用(SPA)：一個入口起點，
   多頁應用(MPA)：多個入口起點。*/
module.exports = {
  entry: () => './demo'
};
  //動態入口
};
```
## **`output`**
> 指示 webpack 如何去輸出、以及在哪裡輸出你的「bundle、asset 和其他你所打包或使用 webpack 載入的任何內容」。
- path: 所有輸出文件的目標路徑
- library: 導出庫(exported library)的名稱
- libraryTarget: 導出庫(exported library)的類型
- chunkfilename:
- filename: 此選項決定了每個輸出 bundle 的名稱。
   -  當通過多個入口起點(entry point)、代碼拆分(code splitting)或各種插件(plugin)創建多個 bundle
```go
module.exports = {
  output: {
    filename: 'bundle.js'
    //只有一個入口時使用此

    filename: '[name].bundle.js'
    //使用入口名稱
    filename: '[id].bundle.js'
    //使用內部 chunk id
    filename: '[name].[hash].bundle.js'
    //使用每次構建過程中，唯一的 hash 生成
    filename: '[chunkhash].bundle.js'
    //使用基於每個 chunk 內容的 hash
  }
};
```
- auxiliaryComment: 
- publicPath: 該選項的值是以 runtime(運行時) 或 loader(載入時) 所創建的每個 URL 為前綴。因此，在多數情況下，此選項的值都會以/結束。
```go
module.exports = {
  output: {
    publicPath: 'https://cdn.example.com/assets/', 
    // CDN（總是 HTTPS 協議）
    publicPath: '//cdn.example.com/assets/', 
    // CDN（協議相同）
    publicPath: '/assets/', 
    // 相對於服務(server-relative)
    publicPath: 'assets/', // 相對於 HTML 頁面
    publicPath: '../assets/', // 相對於 HTML 頁面
    publicPath: '', // 相對於 HTML 頁面（目錄相同）
  }
};
--------------------------------------
<link href="/assets/spinner.gif" />
//對於一個輸出 HTML 的 loader 可能會像這樣輸出
background-image: url(/assets/spinner.gif);
//加載 CSS 的一個圖片時
```
## **`module`**
### **rule**
> 模塊規則（配置 loader、解析器等選項）
### **loader**
- include: 匹配路徑
- test: 匹配檔案格式
- exclude: 必不匹配選項
  - 儘量避免 exclude，更傾向於使用 include
- issuer: { test, include, exclude },導入條件
- loader:對應名稱使用
- options:
```go
 options: {
          presets: ["es2015"]
        },
```
- use: 應用多個 loader 和選項
```go
module.exports = {
  module: {
    rules: [
      {
        use: [
          'style-loader',
          {
            loader: 'css-loader',
            options: {
              importLoaders: 1
            }
          },
          {
            loader: 'less-loader',
            options: {
              noIeCompat: true
            }
          }
        ]
      }
    ]
  }
};
```
## **`plugins`**

```js
  const htmlWebpackPlugin = require('htmlWebpackPlugin');
  //在module.exports前需先加上，才可使用
 plugins: [
    new HtmlWebpackPlugin({
      template: './src/index.html',
      tittle: 'webpack 練習',
      minify:{collapseWhitespace: true,}
      })
  ]
  //tittle 需再html 改為<tittle><%= htmlWebpackPlugin.options.title %></tittle>
```
## **`resolve`**
> 能設置模塊如何被解析。
***

## **各類型loader介紹** (https://webpack.js.org/loaders/)
## **`css-loader`**
- 與style-loader互相使用
   - style-loader的功用是將css模塊導出作為樣式添加到HTML
> css-loader

### **1. 安裝css loader**
> 安裝後package.json會出現版本訊息
```go
$npm install --save-dev css-loader
$npm install --save-dev style-loader
```
### **2. 在webpack.config.js裡指定loader**
```go
module: {
    rules: [
      {
        test: /\.css$/,
        use: [ 'style-loader', 'css-loader' ]
      }
    ]
  }
};
```
### **3. 在.css裡指定loader**
```go
import css from './app.css';
var css = require("css-loader!./file.css");
//
在css檔案@import '~module/styles.css';
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