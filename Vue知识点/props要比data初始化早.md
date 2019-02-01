因为 `props` 要比 `data` 先完成初始化，所以我们可以利用这一点给 `data` 初始化一些数据进去，看代码：
```html
  <script>
    Vue.component('Child', {
      props: {
        size: String
      },
      data () {
        return {
          buttonSize: this.size
        }
      },
      template: '<div :style="{width: buttonSize,backgroundColor: `red`}">{{buttonSize}}</div>',
      created () {
        console.log(this.buttonSize)
      }
    })
    const vm = new Vue({
      el: '#app',
      data: {
        test: 1
      },
      components: ['Child']
    })

  </script>
```