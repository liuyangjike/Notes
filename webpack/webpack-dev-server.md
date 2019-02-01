## webpack-dev-server
>webpack-dev-server主要是启动了一个使用express的Http服务器。它的作用主要是用来伺服资源文件,原始文件作出改动后，webpack-dev-server会实时的编译，但是最后的编译的文件并没有输出到目标文件夹，

><font color=blue>注意：你启动webpack-dev-server后，你在目标文件夹中是看不到编译后的文件的,实时编译后的文件都保存到了内存当中。因此很多同学使用webpack-dev-server进行开发的时候都看不到编译后的文件<font>
```javascript
\\ webpack.config.js
    module.exports = {
        entry: './src/js/index.js',
        output: {
            path: './dist/js',
            filename: 'bundle.js'，
            publicPath: '/assets/'
        }
    }
    //因为webpack-dev-server伺服的文件是相对publicPath这个路径的
```

那么，在index.html文件当中引入的路径也发生相应的变化:
```html
    <!DOCTYPE html>
    <html lang="en">
    <head>
        <meta charset="UTF-8">
        <title>Demo</title>
    </head>
    <body>
        <script src="assets/bundle.js"></script>
    </body>
    </html>
```