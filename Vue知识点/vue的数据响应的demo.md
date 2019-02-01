```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <meta name="viewport" content="width=device-width, initial-scale=1.0">
  <meta http-equiv="X-UA-Compatible" content="ie=edge">
  <title>Document</title>
  <!-- <script type="text/javascript" src="http://vuejs.org/js/vue.min.js"></script> -->
</head>

<body>
  <div id='app'>
    <child @hook:created="handleChildCreated"></child>
  </div>
  <script>
    function walk(data) {
      for (let key in data) {
        const dep = []
        let val = data[key]
        // 如果 val 是对象，递归调用 walk 函数将其转为访问器属性
        const nativeString = Object.prototype.toString.call(val)
        if (nativeString === '[object Object]') {
          walk(val)
        }
        Object.defineProperty(data, key, {
          set(newVal) {
            if (newVal === val) return
            val = newVal
            dep.forEach(fn => fn())
          },
          get() {
            dep.push(Target)
            return val
          }
        })
      }
    }
    const data = {
      name: '霍春阳',
      age: 24
    }
    walk(data)

    function render() {
      return document.write(`姓名：${data.name}; 年龄：${data.age}`)
    }

    let Target = null

    function $watch(exp, fn) {
      Target = fn
      let pathArr,
        obj = data
      // 如果 exp 是函数，直接执行该函数
      if (typeof exp === 'function') {
        exp()
        return
      }
      if (/\./.test(exp)) {
        pathArr = exp.split('.')
        pathArr.forEach(p => {
          obj = obj[p]
        })
        return
      }
      data[exp]
    }
    $watch(render, render)

  </script>

</body>

</html>

```