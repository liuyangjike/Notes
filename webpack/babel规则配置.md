## 配置
1. 安装`babel-loader、babel-core、babel-preset-env, babel-preset-react或.....`
2. 两种方式
>方式一: 通过package.json。在package.json文件中增加一个“babel"属性，该属性是一个JSON对象，作用是设置项目中的babel转码规则和使用到的babel插件
```javascript
"babel": {
    "presets": [
      "react",  // 用babel-preset-react对react解析
      "es2015"  // 用babel-preset-es2015对es2015+解析
    ]
},
```
>第二种:即通过.babelrc文件。在项目根目录下新建.babelrc文件，里面只需输入第一种方式中”babel”属性的值即可
```javascript
{
  "presets": ["es2015"]
}
```