# Object.defineProperty()

首先我们看官方给出的解释是：

**Object.defineProperty()** 方法会直接在一个对象上定义一个新属性，或者修改一个对象的现有属性，并返回此对象。

## 语法

> Object.defineProperty(obj, prop, descriptor)

参数

obj > 要定义的对象

prop > 要定义或修改的属性的名称或 **symbol**

descriptor > 要定义或修改的属性描述符

返回值 > 返回此对象

_例：_

```js
const obj = {};
const descriptor = {
  value: "lucy",
  enumerable: false,
  writable: false,
  configurable: false,
};
Object.defineProperty(obj, "name", descriptor);

console.log(obj.name); // lucy

obj.name = "rose";

console.log(obj.name); // lucy
```

> 默认情况下，使用 Object.defineProperty() 添加的属性值是不可修改（immutable）的

obj和prop没什么好说的，下面主要说说descriptor

## 描述符

对象里目前存在的属性描述符有两种主要形式：**数据描述符**和**存取描述符**。

* **数据描述符**是一个具有值的属性，该值可以是可写的，也可以是不可写的。

* **存取描述符**是由 getter 函数和 setter 函数所描述的属性。

> tips: 一个描述符只能是这两者其中之一；不能同时是两者。

两种描述符都是对象，且共同拥有以下可选键值(默认值是指在使用 Object.defineProperty() 定义属性时的默认值）

configurable --> 当为true的时候，该属性的描述符才可以被改变或者删除，默认为false

enumerable --> 当为true时，该属性才会出现在对象的枚举属性中，默认为false

**数据描述符** 的可选键值

value ---> 该属性对应的值，可以时任何javascript的值, 默认为undefined

writable ---> 当为true时，上面的value才可以被赋值运算符改变,默认为false

**存取描述符** 的可选键值

get ---> 属性的getter函数。当访问该属性的时候，会调用此函数。执行时不传入任何参数，但是会传入this对象(由于继承关系，这里的this不一定时定义该属性的对象) 该函数的返回值会被用着属性的值. 默认undefined

set ---> 属性的setter函数，当属性值被修改时，会调用此函数。该方法接收一个参数(就是被赋予的新值)，会传入赋值时的this对象, 默认undefined

* Vue双向数据绑定原理就是使用的Object.defineProperty()
