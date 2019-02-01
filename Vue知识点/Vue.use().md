## Vue.use源码
```javascript
  Vue.use = function (plugin) {
    var installedPlugins = (this._installedPlugins || (this._installedPlugins = []));
    if (installedPlugins.indexOf(plugin) > -1) {
      return this
    }

    // additional parameters
    var args = toArray(arguments, 1);
    args.unshift(this);
    if (typeof plugin.install === 'function') {
      plugin.install.apply(plugin, args);
    } else if (typeof plugin === 'function') {
      plugin.apply(null, args);
    }
    installedPlugins.push(plugin);
    return this
  };
```
使用`Vue.use(ElementUI)`由上面代码,`plugin`插件可以是一个函数或者对象(包含install属性是个函数),
`element-ui`它s是`export {install...}`, `install`内部是用`Vue.component(name, component)`注册每个组件

## 下面两种实现

### 无install
```javascript
function JI (Vue) {  
  Vue.jike = '留言'
} 
Vue.use(JI)
console.log(Vue.jike) // 取值
```

### 有install
```javascript
function JI(Vue) {
  Vue.liu = '刘扬'
}
var JI2 = {install: JI}

Vue.use(JI2)
console.log(Vue.liu)  // 刘扬

```