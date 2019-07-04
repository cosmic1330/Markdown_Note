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
##Closure 結合 CallBack Funciton
> 利用以上兩個方式，便可取出 一些預設物件方法內的值 ex:ajax

```js
  function formatStoreName(value,row,index){
        //先建立Clouser內的全域變數
        let self='';
        $.ajax({
            type: "POST",
            url: "./getStoreName",
            data: {
                storeId: value,
            },
            async: false,
            success: function (data) {
                //呼叫Clouser的function
                name(data);
            },
            error: function (XMLHttpRequest, textStatus, errorThrown) {
                console.log(errorThrown);
            }
        });
        //建立Clouser的function 方法內回傳原全域變數
        function name(value){
            console.log(value);
            return self=value;
        }
        return self;
	}
```
