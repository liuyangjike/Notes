### 基本数据类型
按照值访问的
### 引用数据类型
存在内存中,按指引访问(类似指针)
### 传递参数
函数传递参数(按照`值`传递)
1.基本数据类型,不会改变外部
2.引用数据类型,会改变外部数据
### 普通对象与函数对象
>凡是通过 new Function() 创建的对象都是函数对象，其他的都是普通对象
### 构造函数
```javascipt
function Person(name, age, job) {
 this.name = name;
 this.age = age;
 this.job = job;
 this.sayName = function() { alert(this.name) } 
}
var person1 = new Person('Zaxlct', 28, 'Software Engineer');
var person2 = new Person('Mick', 23, 'Doctor');
```
person1 和 person2 都是 构造函数 Person 的实例
一个公式：
>实例的构造函数属性（constructor）指向构造函数。
### 原型对象
在 JavaScript 中，每当定义一个对象（函数也是对象）时候，对象中都会包含一些预定义的属性。其中每个函数对象都有一个prototype 属性，这个属性指向函数的原型对象
>每个对象都有 __proto__ 属性，但只有函数对象才有 prototype 属性
>
>原型对象就是 Person.prototype
</br>
>在默认情况下，所有的原型对象都会自动获得一个 constructor（构造函数）属性，这个属性（是一个指针）指向 prototype 属性所在的函数（Person）
>Person.prototype.constructor == Person

<strong>结论：原型对象（Person.prototype）是 构造函数（Person）的一个实例<strong>
### `__proto__`

JS 在创建对象（不论是普通对象还是函数对象）的时候，都有一个叫做__proto__ 的内置属性，用于指向创建它的构造函数的原型对象。
>person1.__proto__ == Person.prototype