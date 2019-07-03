# 閉包
> 閉包是function內的funciton，通常是用來保護某些函數的方法之一;
> 無法直接取得閉包內的參數，閉包內的參數只存在function執行時;
> Vue是一個能將資料與畫面連結的框架工具，配合資料修訂能更便利的更改畫面。
## **`起始式`**
```js
  let const = function(num){
    let const = num++;
    return function(const){
      console.log(const)  
    }
  }
  const(0);
  //得到1
```
