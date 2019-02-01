## iconfont用法
>这里介绍`font-class`这种
>1.下载到本地, 拷贝几种字体的文件到目录(包括css)
>2.在指定的要用到的css引入, 如
```javascript
@import "../../assets/fonts/iconfont.css";
```
>3.设置iconfont标签font-family
```javascript
[class^="icon-"], [class*=" icon-"] {
  font-family:"iconfont";
  font-size:16px;
  font-style:normal;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}
```
>4.在想用icon的标签直接写样式`className=icon-dingdan`