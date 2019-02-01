## 定义
> 在css样式`转换`时生效,转换只是从初始状态到最终状态。您无法像动画一样指定任何中间点，因此如果您尝试创建下一个 `Teen Girl Squad`感觉或复杂动画，则过渡可能不是一个好的选择 。(可以通过事件或者伪类触发)
## 属性
> ### `transition-property`
规定应用过渡效果的 CSS 属性的名称（当指定的 CSS 属性改变时，过渡效果开始），其默认值为all。
> ### `transition-duration`
规定完成过渡效果需要的时间（单位为 s 或 ms），其默认值为 0s ，意味着如果不指定这个属性，将不会呈现过渡效果。
> ### `transition-timing-function`
规定过渡效果的时间曲线。
`ease`: 慢速开始，中间变快，慢速结束；
`linear`: 匀速运动
.....
> ### `transition-delay`
规定过渡效果的延迟时间，默认为 0s 。
```css 
  .c3{
    height: 40px;
    width: 40px;
    background-color: yellow;
    border-radius: 50%;
    transition: width 1s ease,background-color 2s ease;
  }
  .c3:hover{
    width: 80px;
    height: 80px;
    border-radius: 50%;
    background-color: tomato;
  }


```
