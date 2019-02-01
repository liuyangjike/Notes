由于每一次对文档的插入都会引起重新渲染（计算元素的尺寸，显示背景，内容等），所以进行多次插入操作使得浏览器发生了很多次渲染，效率是比较低的。这是我们提倡通过减少页面的渲染来提高DOM操作的效率的原因。
```js
    var ul = document.getElementById('ul')
    for (var i = 0; i < 100; i++) {
      var li = document.createElement('li')
      li.innerHTML = "index " + i
      ul.appendChild(li)
    }
```

因为文档片段存在于内存中，并不在DOM中，所以将子元素插入到文档片段中时不会引起页面回流（对元素位置和几何上的计算），因此使用DocumentFragment可以起到性能优化的作用。例如上面的代码就可以改成下面的
```js
    var ul = document.getElementById('ul')
    var frag = document.createDocumentFragment()

    for (var i =0; i < 100; i++) {
      var li = document.createElement('li')
      li.innerHTML = "index " + i    
      frag.appendChild(li)  
    }
    ul.appendChild(frag)
```