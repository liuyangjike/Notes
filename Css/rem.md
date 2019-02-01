
### rem基准值
* 以一个确定的屏幕来作为参考，这个就由我们拿到的视觉稿来定
* 以iphone6的屏幕为基准设计的
* rem基准值就是37.5(屏幕宽375px, 放下10个字)
## 例子
> 以iphone6为例,宽: `375px`

现在, 设计稿某个按钮宽`100px`
```scss
@function px2rem($px) {
    $rem: 37.5px;
    @return ($px/$rem) + rem;
}
.btn{
    height: px2rem(100px);
}
```
### 利用javascript来动态设置 根据rem算出的基准值
```javascript
(function (doc, win) {  // 自适应
  var docEl = doc.documentElement,
    resizeEvt = 'orientationchange' in window ? 'orientationchange' : 'resize', // 监听手机旋转
    recalc = function () {
      var clientWidth = docEl.clientWidth;
      if (!clientWidth) return;
      docEl.style.fontSize = 20 * (clientWidth / 320) + 'px'; // 放下16个字
    };
  if (!doc.addEventListener) return;
  win.addEventListener(resizeEvt, recalc, false);
  doc.addEventListener('DOMContentLoaded', recalc, false); // 监听dom加载
})(document, window);
```

