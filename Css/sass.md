## sass用法

### 变量
```javascript
$blue : #1875e7;
div {
    color: $blue;
}
```
变量套在字符串里
```javascript
$side : left;
.rounded {
    border-#{$side}-radius: 5px;
}
```

### 计算
```javascript
body {
    margin: (14px/2);
    top: 50px + 100px;
    right: $var * 10%;
}
```

### 引用父标签

```javascript
a {
   &:hover { color: #ffb3ff; }
}
```

### 继承
```javascript
.class1 {
    border: 1px solid #ddd;
}
.class2 {
    @extend .class1;
    font-size:120%;
}
```

### mixin代码块复用
```javascript
// 定义
@mixin flex($justify-content: center, $align-items: center) {
  display: flex;
  justify-content: $justify-content;
  align-items: $align-items;
}

@mixin font($font-size, $color: #333, $text-align: left) {
  font-size: $font-size;
  color: $color;
  text-align: $text-align;
}

@mixin wh($w, $h){
  width: $w;
  height: $h;
}

//使用
@include font($font-size: 30px, $text-align: center);
@include wh(100%, 100%);

```

### 循环
```javascript
@for $i from 1 to 10 {
    .border-#{$i} {
        border: #{$i}px solid blue;
    }
}
```