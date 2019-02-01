### sort方法排序

简单数字
```js
function sortNumber(a,b) {
    return a - b
}
var list = [3, 1, 51, 13, 6]
list.sort(sortNumber) // [1, 3, 6, 13, 51]
```
数组对象
```js
var arr = [
{name:'zopp', age:1},
{name:'gpp', age: 13},
{name: 'yuu', age: 5}
]
function compare(property){
    return function (a, b) {
        var value1 = a[property]
        var value2 = b[property]
        return value1 - value2
    }
}
arr.sort(compare('age'))
```

### 冒泡排序

```js
var list = [9, 2, 4, 12, 51, 23, 53, 39]
    function sort(list) {
      for (i = 0; i < list.length -1;i++){
        for (j = 0; j < list.length - 1 -i; j++) {
          if (list[j] > list [j+1]) {
            var temp = list [j]
            list[j] = list[j+1]
            list[j+1] = temp
          }
        }
      }
      return list
    }
  sort(list)
```
里面的循环,找出最大的排,外未排序过的最后,外面循环是表示执行多少次排最大的