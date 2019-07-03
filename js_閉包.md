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


```js
 function throttling(func, wait = 20, immediate = true) {
        var timeout;
        return function() {
          var context = this,
            args = arguments;
          var later = function() {
            timeout = null;
            // if (!immediate)
            func.apply(context, args);
          };
          if (timeout) return;
          var callNow = immediate && !timeout;
          clearTimeout(timeout);
          timeout = setTimeout(later, wait);
          if (callNow) func.apply(context, args);
        };
      }

      let images = document.querySelectorAll("img");
      function scrollHandler() {
        let windowTop = window.scrollY;
        let windowBottom = windowTop + window.innerHeight;
        images.forEach(img => {
          let imgMiddle = img.offsetTop + img.height / 2;
          if (imgMiddle < windowBottom && imgMiddle > windowTop) {
            img.classList.add("active");
          } else {
            img.classList.remove("active");
          }
        });
      }

      window.addEventListener("scroll", throttling(scrollHandler));
```
