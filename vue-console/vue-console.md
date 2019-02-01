## 前言
本文通过console.log的一些特性,结合vue.js的源码,通过一个简单的例子,让你了解Vue的各个过程的变化.
效果图


>请用chrome查看,并打开控制台看效果
[演示地址](http://www.vue-console.xyz/)

## 准备
### `vue-console.html`的创建
下载`vue.js`文件,在`vue-console.html`中引入,我写了一个简单的例子,涵盖:初始化视图->点击后更新视图(包括各个钩子函数)
代码如下:
```html
  <script src="./vue.js"></script>
  <div id="app">
    <div id="hi" @click="changeName">{{name}}</div>
  </div>
  </div>
    <script>
    var style = 'font-size: 20px;color: blue'
    var vm = new Vue({
      el:'#app',
      data() {
        return {
          name: '点我',
        }
      },
      beforeCreate () {
        console.log('%cI am beforeCreate------ 我在选项里写的', style)
      },
      created () {
        console.log('%cI am created------ 我在选项里写的', style)
      },
      beforeMount () {
        console.log('%cI am beforeMount------ 我在选项里写的', style)
      },
      mounted () {
        console.log('%cI am mounted------ 我在选项里写的', style)
      },
      beforeUpdate () {
        console.log('%cI am beforeUpdate------ 我在选项里写的',style)
      },
      updated () {
        console.log('%cI am updated------ 我在选项里写的', style)
      },
      methods: {
        changeName () {
          this.name = 'jike'
        } 
      }
    })  
  </script>
```

### console.log样式的配置
```javascript

var tagLeftStyle = [
  'color: #fff',
  'border-top-left-radius:3px',
  'border-bottom-left-radius:3px',
  'background-color: #564b4f',
  'padding: 5px'
].join(';')

var tagRightStyle = function (color) {
  color = color?color:'#0BCF1B'
  return [
    'color: #fff',
    'border-top-right-radius:3px',
    'border-bottom-right-radius:3px',
    `background-color: ${color}`,
    'padding: 5px'
  ].join(';')
}
// ...
// 一些样式省略,具体可以去看源码
var tagVariable = function (obj, tag, desc, num, detail, color) {
  console.log(`%c${lineNo} %o%c<---%c${tag}%c${desc}  %c源码${num}行 %c说明: %o`, noStyle, obj, arrowStyle ,tagLeftStyle, tagRightStyle(color), sourceNoStyle, detailStyle, detail)
  lineNo++
}
// %c代表后面的文本,使用css样式,%o代表对象输出
```
上面的代码只要调用`tagVariable(...)`传递参数,就实现上图的标签效果,
还可以`console.log`一下图片方便理解;
通过调用上面封装的函数在`vue.js`某些时刻调用,就达到很好演示效果


## 开始
我将整个过程分为四个阶段: 构造函数阶段、初始化阶段、挂载阶段 、更新阶段,
会以上面提到的例子贯穿的
### 构造函数阶段
平常我们使用`Vue`,都是用`new Vue({})`,其实就是调用它的构造函数创建实例.

### 初始化阶段
会对我们传入`data`、`methods`等处理,便于后面阶段的调用及一些功能的实现
如例子的`data`的`name`会被代理到`vm`实例上,所以我们可以用`this.name`调用
```javascript
data() {
  return {
    name: '点我',
  }
}
```

### 挂载阶段
```javascript
<div id="app">
  <div id="hi" @click="changeName">{{name}}</div>
</div>
```
会将上面的`html`渲染成页面(这里面包括渲染函数,虚拟的实现等)

### 更新阶段
点击页面上的文本时发生更新,这个过程包括:wathcer的触发、patch算法对比新旧Vnode,更新dom

## 说明
具体的可以去看源码,在[github](https://github.com/liuyangjike/vue-console)上,觉得可以的话帮忙star一下

参考文章: [Vue技术内幕](http://hcysun.me/vue-design/)
[Vue.js 源码解析](https://github.com/answershuto/learnVue)