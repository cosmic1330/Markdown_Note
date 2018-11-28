# Vue 
[img01]:/image/Vue.jpg "Vue圖片"
![Vue圖片][img01]
> Vue是一個能將資料與畫面連結的框架工具，配合資料修訂能更便利的更改畫面。
## **`起始式`**
```js
var app = new Vue({
  el: '#app',
  delimiters = ['${', '}'],  //可將{{}}符號改為S{}
  data: {
    message: 'Hello Vue!'
  },
  //data 可以是 object 或 function，但元件（component）的 data 只能是 function，這是因為元件內各自擁有自己的 data，而非共用的關係。
  methods: {
    reverseMessage: function () {
      this.message = this.message.split('').reverse().join('')
    }
  },
})
```
## **`Vue基本使用`**
###  **1. {{ }}:**
> 與v-model、v-bind的用法類似，都是用於綁定data
###  **2. V-bind:**
> v-bind可綁定屬性，沒有雙向綁定效果，可在任何元素中使用。＊:是v-bind的縮寫
```go
<p v-bind:src="http://...."></p>
<p v-bind="message"></p>
<div v-bind:class="{ active: isActive }"></div>
```
###  **3. V-if**
> 通常與v-else合用

###  **4. v-for**
> v-for可設定第二個參數為索引值
```go
<div id="app">
  <ul>
    <li v-for="(item, key, index) in list">
      index: ${ index },
      key: ${ key },
      name: ${ item.name }
    </li>
  </ul>
</div>
<!-- 顯示 
index:0,key:123456789,name:選項1
index:1,key:234567890,name:選項2
index:2,key:345678901,name:選項3

//V-fot使用常數
<div>
  <span v-for="n in 10">${ n }</span>
</div>
<!-- 1 2 3 4 5 6 7 8 9 10 -->
-->
```
```js
var vm = new Vue({
  el: '#app',
  delimiters: ['${', '}'],
  data: {
    list: {
      '123456789': { name: '選項 1' },
      '234567890': { name: '選項 2' },
      '345678901': { name: '選項 3' }
    }
  }
});
```
###  **5. v-model**
> 和data合作實現雙向綁定，只能用於表單元素。
###  **6. v-on**
> 可綁定事件，執行function ＊@是v-on的縮寫
```js
<div id="app-5">
  <p>{{ message }}</p>
  <button v-on:click="reverseMessage">Reverse Message</button>
</div>
```
###  **7. computed**
>
## **`優先權`**
### **v-for的優先權高於v-if**
> 先執行後再判斷
```js
<ul>
  <li v-if="n % 2 === 1" v-for="n in 10">${ n }</li>
</ul>
```
### **v-model的優先權高於v-bind**
***