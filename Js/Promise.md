谓`Promise`，简单说就是一个容器，里面保存着某个未来才会结束的事件（通常是一个异步操作）的结果。从语法上说，`Promise` 是一个对象，从它可以获取异步操作的消息。`Promise` 提供统一的 `API`，各种异步操作都可以用同样的方法进行处理。
```js

var test = 1
  const promise = new Promise((resolve, reject) => {
          setTimeout(()=> {
            if (this.test === 1) {
              resolve('success')
            } else {
              reject('error')
            }
          }, 8000)
        })
           promise.then((val)=> {
          console.log(val) // 'success'
        }, (err)=> {
          console.log(err)
        })
```