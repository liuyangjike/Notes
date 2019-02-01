## babel-loader
>loader 可以将所有类型的文件转换为 webpack 能够处理的有效模块，然后你就可以利用 webpack的打包能力，对它们进行处理.虽然webpack本身就能够处理.js文件，但无法对ES2015+的语法进行转换，babel-loader的作用正是实现对使用了ES2015+语法的.js文件进行处理
## babel-core
>把 js 代码分析成 ast (抽象语法树, 是源代码的抽象语法结构的树状表现形式)，方便各个插件分析语法进行相应的处理。有些新语法在低版本 js 中是不存在的，如箭头函数，rest 参数，函数默认值等，这种语言层面的不兼容只能通过将代码转为 ast，再通过语法转换器分析其语法后转为低版本 js。
<font color=blue>babel-core的作用在于提供一系列api。这便是说，当webpack使用babel-loader处理文件时，babel-loader实际上调用了babel-core的api</font>
## babel-preset-*
>`babel-preset-*`的作用是告诉babel使用哪种转码规则进行文件处理。事实上，babel有几种规则都可以实现对ES6语法的转码，如babel-preset-es2015、babel-preset-latest、babel-preset-env

注意: <font color=red>babel-core与babel-loader的版本要匹配<font>