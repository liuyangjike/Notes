## 前言
随着前端的三大框架的出现,组件化的思想越来越流行,出现许多组件库.它能够帮助开发者节省时间提高效率,<br>
如React的Ant-design,Vue的iView,Element等,它们的功能已经很完善了.我写这遍文章的目的:记录自己搭建UI库的过程(对Vue的理解加深了好多)[*演示地址*](http://www.goingtrace.com)<br>
*首先讲一下思路:*
平常写组件时,写一个组件要用时直接导入就行了,如你写了一个time.vue,用的时候
```javascript
import time from '路径'
```

现在要写一个组件库,是不是把所有组件一个文件夹里(如`button.vue`,`icon.vue`,`input.vue`...),通过`Vue.components`注册所有组件,再通过`Vue.use()`安装一下就实现了
这就是所以的`vue`插件的思路,没有那么神秘
## 1.环境准备
前面说要把所有的组件放在一个文件夹里,最简单就是用脚手架搭一个项目目录结构,同时还需要添加示例文档----方便调试和展示:<br>
*按钮的示例效果*

![](https://user-gold-cdn.xitu.io/2018/8/30/1658a21309d3cb17?w=834&h=408&f=png&s=129209)
现在要考虑比较重要的两点:**目录结构**和**示例文档**<br>
1.目录结构
 直接用vue-cli建立项目结构, 在基础上修改一下就行了(以满足我们示例的展示)<br>
*目录结构*
```javascript
.
├── build  -------------------------webpack相关配置文件
│   ├── build.js
│   ├── check-versions.js
│   ├── logo.png
│   ├── strip-tags.js
│   ├── utils.js
│   ├── vue-loader.conf.js
│   ├── webpack.base.conf.js -------配置markdown设置时会用到它
│   ├── webpack.dev.conf.js
│   └── webpack.prod.conf.js
├── config  ------------------------vue的基本配置
│   ├── dev.env.js
│   ├── index.js
│   └── prod.env.js
├── examples -----------------------放置例子
│   ├── App.vue --------------------根文件
│   ├── assets ---------------------静态资源
│   │   ├── css --------------------css
│   │   ├── img --------------------图片
│   │   └── logo.png ---------------vue的logo
│   ├── components -----------------公共组件
│   │   ├── demo-block.vue ---------盒子组件
│   │   ├── footer.vue -------------footer组件
│   │   ├── header.vue -------------header组件
│   │   └── side-nav.vue -----------侧边栏组件
│   ├── docs -----------------------例子模块的文档
│   │   ├── breadcrumb.md ----------面包屑组件文档
│   │   ├── button.md --------------按钮组件文档
│   │   ├── card.md ----------------卡片组件文档
│   │   ├── guide.md ---------------简介文档
│   │   ├── icon.md ----------------图标文档
│   │   ├── install.md -------------安装文档
│   │   ├── layout.md --------------布局文档
│   │   ├── logs.md ----------------更新日志文档
│   │   ├── message.md -------------消息文档
│   │   ├── start.md ---------------快速开始1文档
│   │   ├── tag.md -----------------标签文档
│   │   └── twotable.md ------------二维表格文档
│   ├── icon.json ------------------图标数据
│   ├── main.js --------------------入口文件
│   ├── nav.config.json ------------侧边栏数据
│   └── router ---------------------路由
│       └── index.js ---------------路由配置
├── packages -----------------------组件库源代码
│   ├── README.md ------------------README
│   ├── breadcrumb -----------------面包屑源码
│   │   ├── index.js
│   │   └── src
│   ├── breadcrumb-item ------------面包屑源码
│   │   └── index.js
│   ├── button ---------------------按钮源码
│   │   ├── index.js
│   │   └── src
│   ├── card -----------------------卡片源码
│   │   ├── index.js
│   │   └── src
│   ├── col ------------------------列布局源码
│   │   ├── index.js
│   │   └── src
│   ├── message --------------------消息源码
│   │   ├── index.js
│   │   └── src
│   ├── two-dimensional-table -----二维表格源码
│   │    ├── index.js
│   │    └── src
│   ├── row -----------------------行源码
│   │   ├── index.js
│   │   └── src
│   ├── tag -----------------------标签源码
│   │   ├── index.js
│   │   └── src
│   ├── theme-default --------------样式表
│   │   └── lib
│   ├── package.json
│   └── index.js -------------------组件库入口
├── index.html ---------------------主页
├── package.json
├── static
└── README.md
```
以上是已经修改过的目录结构,将脚手架生成的src目录改为examples用来放示例文档,所以相应的你要修改build目录下的webpack.base.conf.js ,
让它指向examples,webpack才能正确进行打包

![](https://user-gold-cdn.xitu.io/2018/8/30/1658a233dba2de19?w=937&h=264&f=png&s=43685)
2. 示例文档
编写文档使用markdown最适合了,要让vue能够实现markdown文档可以用[vue-markdown-loader](https://github.com/QingWei-Li/vue-markdown-loader),配置相关文件
在webpack.base.conf.js 的rules里添加

![](https://user-gold-cdn.xitu.io/2018/8/30/1658a23e141975ba?w=783&h=118&f=png&s=17436)
就可以开始写文档,测试一下
```javascript
{
  path: '/hello',
  name: 'hello',
  component: r => require.ensure([], () => r(require('../docs/hello.md')))          
}
```
npm run dev 跑项目打开http://localhost:8080/#/hello,  可以显示,初步成功(基本实现)
接下来就要实现示例文档的效果: **既能演示又有代码展示**(如下图)

![](https://user-gold-cdn.xitu.io/2018/8/30/1658a259bcd1b91d?w=934&h=566&f=png&s=230665)

如上图示例文档是button.md要让它在button.md一个文件里想显示代码的地方显示代码,想显示按钮的地方显示按钮,所以就要在显示按钮的地方打上一个标识符,

让编译过程中能够识别,安装.vue的方式编译展示
还是要用到markdown的配置,它其实封装了[markdown-it](https://github.com/markdown-it/markdown-it),支持options选项,只要加上定义的标识符(我用的是'demo'),options 选项的配置(也在webpack.base.conf.js 里)

```javascript
const vueMarkdown = {
  preprocess: (MarkdownIt, source) => {
    MarkdownIt.renderer.rules.table_open = function () {
      return '<table class="table">'
    }
    MarkdownIt.renderer.rules.fence = utils.wrapCustomClass(MarkdownIt.renderer.rules.fence)
    const code_inline = MarkdownIt.renderer.rules.code_inline
    MarkdownIt.renderer.rules.code_inline = function (...args) {
      args[0][args[1]].attrJoin('class', 'code_inline')
      return code_inline(...args)
    }
    return source
  },
  use: [
    [MarkdownItContainer, 'demo', {
      // 用于校验包含demo的代码块
      validate: params => params.trim().match(/^demo\s*(.*)$/),
      render: function (tokens, idx) {

        var m = tokens[idx].info.trim().match(/^demo\s*(.*)$/);
        if (tokens[idx].nesting === 1) {
          var desc = tokens[idx + 2].content;
          // 编译成html
          const html = utils.convertHtml(striptags(tokens[idx + 1].content, 'script'))
          // 移除描述，防止被添加到代码块
          tokens[idx + 2].children = [];
          return `<demo-block>
                        <div slot="desc">${html}</div>
                        <div slot="highlight">`;
        }
        return '</div></demo-block>\n';
      }
    }]
  ]
}
```
其实这就是把要当解析器遇到带demo的标识符时就会添加我们准备好的demo-block组件,按照以上规则解析成AST(抽象语法树),再把它编译成html
所以写示例文档时,可以这样写

![](https://user-gold-cdn.xitu.io/2018/8/30/1658a2acf00c5b26?w=822&h=994&f=png&s=171215)
## 2.如何编写组件源码
其实没有想象中那么难,就像平常写组件那样,只不过要按照一定结构编写(具体的可以去看我的[github](https://github.com/liuyangjike/JKUI)),一般的UI组件库都支持全局引入和单个组件引入,
全局引入:
```javascript
const install = function(Vue) {
  if(install.installed) return
  components.map(component => Vue.component(component.name, component))
}
```
遍历你写的组件,通过Vue.component注册到Vue上,构成一个install函数,暴露install,当你的别的项目要用时只要安装一下包,用Vue.use()使用(像别的插件一样)
单个文件引入:
```javascript
export default {
  install,
  JButton,
  JCol,
  JRow,
  JTag,
  JBreadcrumb,
  JBreadcrumbItem,
  JCard,
  towTable
}
```
类似的只要暴露出组件就OK了

*别人要能够通过npm安装包用我们的包,我们是不是要在包里写所以组件和样式,别人只要npm安装包和引入一个全部组件的样式两步骤就可以使用了*
## 3. npm发布你的UI框架
1. 你要拥有一个npm账号(没有的直接去官网注册一个)

2. 打开终端登录npm
```javascript
npm login
```
3.发布包
我们只有发布packages这个文件夹就行,写好packages文件夹下个的package.json
```javascript
{
  "name": "jk-ui",
  "version": "1.0.9",
  "description": "UI base on Vue",
  "main": "index.js",
  "scripts": {
    "test": "echo \"Error: no test specified\" && exit 1"
  },
  "repository": {
    "type": "git",
    "url": "git+ssh://git@github.com/liuyangjike/JKUI.git"
  },
  "keywords": [
    "UI"
  ],
  "author": "Jike",
  "license": "ISC",
  "bugs": {
    "url": "https://github.com/liuyangjike/JKUI/issues"
  },
  "homepage": "https://github.com/liuyangjike/JKUI#readme"
}
```
使用npm publish发布就OK了,别人就可以用npm install jk-ui --save愉快的玩耍了
具体的可以去看源码,在[github](https://github.com/liuyangjike/JKUI)上,觉得可以的话帮忙star一下