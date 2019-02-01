```js
var a = 1
var b = 2
const f = new Function('return a && b')
console.log(f()) // 2
```