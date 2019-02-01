## class绑定
### 对象语法
```html
<div class="static"
     v-bind:class="{ active: isActive, 'text-danger': hasError }">
</div>
<script>
    data: {
        isActive: true,
        hasError: true
    }
</script>
```
结果渲染为
```html
<div class="static active text-danger"></div>
```
绑定的数据对象不必内联定义在模板里：
```html
<div v-bind:class="classObject"></div>
<script>
    data: {
  classObject: {
    active: true,
    'text-danger': false
  }
}
</script>
```
渲染的结果和上面一样。我们也可以在这里绑定一个返回对象的`计算属性`。这是一个常用且强大的模式：

### 数组语法
```html
<div v-bind:class="[activeClass, errorClass]"></div>
<script>
    data: {
        activeClass: 'active',
        errorClass: 'text-danger'
    }
</script>
```
## 绑定Style样式
### 对象语法
```html
<div v-bind:style="{ color: activeColor, fontSize: fontSize + 'px' }"></div>
<script>
    data: {
  activeColor: 'red',
  fontSize: 30
}
</script>
```
当然也可以用数组和对象