### 

文件目录
![299614dd52c125527bc50b5967bca8a3.png](evernotecid://AAA8D550-EDFF-4B4C-8E60-A388FFD29BBF/appyinxiangcom/21491229/ENResource/p29)


代码
```javascript
var express = require('express')
var path = require('path')
var app = express()


app.use(express.static(path.join(__dirname, 'dist'))) // 方法1:静态文件

// app.use('/', (req, res, next) => {  // 方法2:传送html
//   res.sendFile(path.join(__dirname, '/public/hash.html'))
// })

app.listen(3000, () => {
  console.log('listening at 3000')
})
```