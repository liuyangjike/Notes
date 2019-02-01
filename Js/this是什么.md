### 正文
`this` 允许复用函数时使用不同的上下文。换句话说，<strong>`this` 关键字允许在调用函数或方法时决定哪个对象应该是焦点</strong>
</br>
第一个也是最重要的问题是“这个函数在哪里被调用？”。判断 `this` 引用什么的 唯一 方法就是看使用 `this` 关键字的这个方法在哪里被调用的
判断 `this` 关键字引用什么也是同样的道理，你甚至可以把 `this` 当成一个普通的函数参数对待 — 它会随着函数调用方式的变化而变化。
### 四条规则
* 隐式绑定
* 显示绑定
* new绑定
* window绑定

### 隐式绑定
请记住，这里的目标是查看使用 `this` 关键字的函数定义，并判断 `this` 的指向。执行绑定的第一个也是最常见的规则称为 隐式绑定。`80%` 的情况下它会告诉你 `this` 关键字引用的是什么
```js
const user = {
  name: 'Tyler',
  age: 27,
  greet() {
    alert(`Hello, my name is ${this.name}`)
  }
}
```
现在，如果你要调用 `user` 对象上的 `greet` 方法，你会用到点号
```js
user.greet()
```
这就把我们带到隐式绑定规则的主要关键点。为了判断 `this` 关键字的引用，函数被调用时先看一看点号左侧。如果有“点”就查看点左侧的对象，这个对象就是 this 的引用。
在上面的例子中，`user` 在“点号左侧”意味着 `this` 引用了 user 对象。所以就好像 在 `greet` 方法的内部 `JavaScript` 解释器把 `this` 变成了 `user`。
我们来看一个类似但稍微高级点的例子
```js
const user = {
  name: 'Tyler',
  age: 27,
  greet() {
    alert(`Hello, my name is ${this.name}`)
  },
  mother: {
    name: 'Stacey',
    greet() {
      alert(`Hello, my name is ${this.name}`)
    }
  }
}
```
现在问题变成下面的每个函数调用会警告什么？
```js
user.greet()
user.mother.greet()
```
每当判断 `this` 的引用时，我们都需要查看调用过程，并确认“点的左侧”是什么。第一个调用，`user` 在点左侧意味着 `this` 将引用 `user`。第二次调用中，`mother` 在点的左侧意味着 `this` 引用 `mother`。
```js
user.greet() // Tyler
user.mother.greet() // Stacey
```
如前所述，大约有 `80%` 的情况下在“点的左侧”都会有一个对象。这就是为什么在判断 `this` 指向时“查看点的左侧”是你要做的第一件事。但是，如果没有点呢？这就为我们引出了下一条规则 —
### 显示绑定
如果 greet 函数不是 user 对象的函数，只是一个独立的函数。
```js
function greet () {
  alert(`Hello, my name is ${this.name}`)
}

const user = {
  name: 'Tyler',
  age: 27,
}
```
我们怎样能让 `greet` 方法调用的时候将 `this` 指向 `user` 对象？。我们不能再像之前那样简单的使用 `user.greet()`，因为 `user` 并没有 `greet` 方法。在 `JavaScript` 中，每个函数都包含了一个能让你恰好解决这个问题的方法，这个方法的名字叫做 `call`。
>“call” 是每个函数都有的一个方法，它允许你在调用函数时为函数指定上下文。
考虑到这一点，用下面的代码可以在调用 `greet` 时用 `user` 做上下文。
```js
greet.call(user)
```
再强调一遍，`call` 是每个函数都有的一个属性，并且传递给它的第一个参数会作为函数被调用时的上下文。换句话说，this 将会指向传递给 `call` 的第一个参数。
显示了如何将参数传递给使用 `.call` 调用的函数。不过你可能注意到，必须一个一个传递 `languages` 数组的元素
可以用数组传参而且 `.apply` 会在函数中为你自动展开。
到目前为止，我们学习了关于 `.call` 和 `.apply` 的“显式绑定”规则，用此规则调用的方法可以让你指定 this 在方法内的指向。关于这个规则的最后一个部分是 `.bind`。`.bind` 和 `.call` 完全相同，除了不会立刻调用函数，而是返回一个能以后调用的新函数。因此，如果我们看看之前所写的代码，换用 `.bind`，它看起来就像这样
```js
function greet (lang1, lang2, lang3) {
  alert(`Hello, my name is ${this.name} and I know ${lang1}, ${lang2}, and ${lang3}`)
}

const user = {
  name: 'Tyler',
  age: 27,
}

const languages = ['JavaScript', 'Ruby', 'Python']

const newFn = greet.bind(user, languages[0], languages[1], languages[2])
newFn() // alerts "Hello, my name is Tyler and I know JavaScript, Ruby, and Python"
```
### new绑定
第三条判断 this 引用的规则是 new 绑定。若你不熟悉 JavaScript 中的 new 关键字，其实每当用 new 调用函数时，JavaScript 解释器都会在底层创建一个全新的对象并把这个对象当做 this。如果用 new 调用一个函数，this 会自然地引用解释器创建的新对象
```js
function User (name, age) {
  /*
    JavaScript 会在底层创建一个新对象 `this`，它会代理不在 User 原型链上的属性。
    如果一个函数用 new 关键字调用，this 就会指向解释器创建的新对象。
  */

  this.name = name
  this.age = age
}

const me = new User('Tyler', 27)
```
### window绑定
假如我们有下面这段代码
```js
function sayAge () {
  console.log(`My age is ${this.age}`)
}

const user = {
  name: 'Tyler',
  age: 27
}
```
如前所述，如果你想用 `user` 做上下文调用 `sayAge`，你可以使用 `.call、.apply` 或 `.bind`。但如果我们没有用这些方法，而是直接和平时一样直接调用 `sayAge` 会发生什么呢？
```js
sayAge() // My age is undefined
```
不出意外，你会得到 `My name is undefined`，因为 this.age 是 `undefined`。事情开始变得神奇了。实际上这是因为点的左侧没有任何东西，我们也没有用 `.call、.apply、.bind `或者 `new` 关键字，JavaScript 会默认 `this` 指向 `window` 对象。这意味着如果我们向 `window` 对象添加 `age` 属性并再次调用 `sayAge` 方法，`this.age` 将不再是 `undefined` 并且变成 `window` 对象的 `age` 属性值。不相信？让我们运行这段代码
```js
window.age = 27

function sayAge () {
  console.log(`My age is ${this.age}`)
}
```
非常神奇，不是吗？这就是第 4 条规则为什么是 `window` 绑定 的原因。如果其它规则都没满足，`JavaScript`就会默认 `this` 指向 `window` 对象。
