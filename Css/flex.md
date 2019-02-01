## flex布局
### 容器属性flex-content
justify-content属性定义了项目在主轴上的对齐方式。
```html
.container{
  display: flex;
  height: 70px;
  align-items: center;
  justify-content: space-between;
  background-color: blueviolet;
}
.container div{
  border: 1px solid #aaa;
  text-align: center;
}
<div class="container">
    <div style="width: 100px;margin-left: 20px;">1</div>
    <div style="width: 100px;">2</div>
    <div style="width: 200px; margin-right: 20px">3</div>
</div>
```
效果
![8cccd8d491a795c0832e59c707c9d934.png](evernotecid://AAA8D550-EDFF-4B4C-8E60-A388FFD29BBF/appyinxiangcom/21491229/ENResource/p2)

### 项目属性flex-grow
flex-grow属性定义项目的放大比例，默认为0，即如果存在剩余空间，也不放大。
```html
.container{
  display: flex;
  height: 100px;
  align-items: center;
  background-color: blueviolet;
}
.container div{
  border: 1px solid #aaa;
  flex: 1;
  text-align: center;
}
<div class="container">
    <div>1</div>
    <div>2</div>
    <div>3</div>
</div>
```
效果
![ecc6b1bba655f99a1a65edbcdc29bf27.png](evernotecid://AAA8D550-EDFF-4B4C-8E60-A388FFD29BBF/appyinxiangcom/21491229/ENResource/p1)
