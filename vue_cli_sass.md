# 在Vue-cli中使用Sass
## 1. 步驟一 安裝
> npm install sass-load node-sass -d
就可以直接使用`import '@/style.scss'`引進檔案到js檔編譯

## 2. 步驟二 結構

> 預設CSS檔建立在components中，使用`<style src="./style.css" scoped></style>`在.vue檔中引入樣式，而使用Sass檔時可以放在assets中也可以放在components中
### **Sass在assets的結構及引用**
在assets中建立 sass的結構資料夾
!['In_assets'][/image/sass1.png]
並在App.vue中引用
![App.vue][/image/sass2.png]

優點：
缺點：

### **Sass在components的結構及引用**
在components中建立sass檔案，依原生的vue component建立結構
!['In_component'][/image/sass3.png]
並在.vue中引用
![App.vue][/image/sass4.png]

優點：
缺點：


