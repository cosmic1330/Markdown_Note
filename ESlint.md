## 安裝 ESlint
>
```go
$npm install eslint -g
```
## 初始化 ESLint
>
```go
$eslint --init
```
- 初始化完畢後目錄下會多一個 .eslintrc.js，裡面就是 ESLint 的設定
- 初始化後，記得在編輯器中安裝Eslint外掛，才會讀取.eslintrc.js檔案
## ESlint的使用
### 1. env
> 要在哪些環境執行，譬如說如果你的程式沒有要在瀏覽器執行，那就不應該有 window 或是 document 物件。
### 2.extends
>
### 3.plugins
>
### 4.rules
> 如果上面的 extends 或是 plugins 有你不想要的規則，這時候就可以用 rules 把它蓋掉，譬如說這邊設定 quotes: ["error", "single"]

## ESlint 在Node.js環境執行
>  使用$npm run lint執行
```go
"scripts": {
    "lint": "eslint src/*.js" //分析錯誤
    "fixed": "eslint --fix src/*.js" //自動修正錯誤
}
```
## 設定Git Commit前遷執行ESlint
> 在 package.json 加上 "pre-commit": ["lint"] 就完成了
```go
"scripts": {
    "lint": "eslint src/*.js" //分析錯誤
    "fixed": "eslint --fix src/*.js" //自動修正錯誤
},
"pre-commit": ["lint"],
```