```js
render: function (createElement) {
    return createElement(
        / 一个 HTML 标签字符串，组件选项对象，或者
  // 解析上述任何一种的一个 async 异步函数。必需参数。
        'div',
        // {Object}
  // 一个包含模板相关属性的数据对象
  // 你可以在 template 中使用这些特性。可选参数。
          {
            'class': {
                foo: true,
                bar: false
            },
              // 和`v-bind:style`一样的 API
              // 接收一个字符串、对象或对象组成的数组
            style: {
                color: 'red',
                fontSize: '14px'
            },
            on: {
                click: this.clickHandler
            },
          },
          // 子虚拟节点 (VNodes)，由 `createElement()` 构建而成，就上上面div的字元素
  // 也可以使用字符串来生成“文本虚拟节点”。可选参数。
          [
            '先写一些文字',
            createElement('h1', '一则头条'),
            createElement(MyComponent, {
              props: {
                someProp: 'foobar'
              }
            })
          ]
          
    )
}
```
