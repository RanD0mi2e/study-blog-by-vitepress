# JavaScript知识点

## js中数据类型以及存储差别

### js中数据类型：

1.原始值：String，Number，Boolean，undefined，null，symbol

``` js
// Number类型可以是十进制、八进制、十六进制
let num = 10086 // 10
let num = 072 // 8
let num = 0x52 // 16
let num = 0 / 0 // NaN，表示返回结果非数字
let num = 3.14e3 // 3140，等价于3.14 * 10^3

// String是不可变的，一旦创建就无法更改
let str1 = 'hello'
str1 = str1 + 'world' // 会把原有str1销毁，创建新的str1并赋值

// null表示对象空指针，虽然是原始值，但是typeof null的结果是 'object'
let car = null
typeof car // 'object'
// undefined由null派生而来
null == undefined // true

// Boolean存在一些隐式转换
if(express) { ... }
其中express为false的隐式转换有： '', 0, null, undefined, NaN;
其中express为true的隐式转换有：非空字符串，非零数值，任意对象

// Symbol （符号）是原始值，且符号实例是唯一、不可变的。符号的用途是确保对象属性使用唯一标识符，不会发生属性冲突的危险
let genericSymbol = Symbol();
let otherGenericSymbol = Symbol();
console.log(genericSymbol == otherGenericSymbol); // false
```

2.引用值：Object，Array，Function，Set，Map，WeakMap，WeakSet

这里专门提一下函数的三种表达方式：

```js
// 1.函数声明
function fn() {}
// 2.函数表达式
const fn = function () {}
// 3.箭头函数
const fn = () => {}
```

### 存储区别：

1.原始值存储在栈内存空间，变量存的是值；

2.引用值存储在堆内存空间，变量存的是指针。

## 数组常用方法

### 1.操作方法

#### 增：

push：插入数组尾部，unshift：插入数组头部，splice：插入数组指定位置，concat：返回拼接后数组副本。

#### 删：

pop：弹出数组尾部，shift：弹出数组首部，splice：删除数组指定元素，slice：返回子数组副本

#### 查：

indexOf：查找元素索引，找不到返回-1

includes：查找元素，返回boolean

find：查找元素，返回找到的元素

findIndex：查找元素，返回找到元素所在数组的索引

#### 改：

splice

### 2.排序方法：

sort(comparator): 接受一个比较器，根据比较器控制排序规则

reverse(): 数组倒序排序

### 3.转换方法

join：把数组转换成字符串

### 4.遍历方法

1.forEach：传入每项都执行回调，没有返回值

2.filter：数组每项都执行回调，返回true的项构成的数组

3.map：数组每项都执行回调，返回函数调用结果组成的数组

4.every：数组每项都执行回调，所有元素返回true，结果返回true

5.some：数组每项都执行回调，至少一个元素返回true，结果返回true

## 字符串常用方法

### 1.操作方法

下列修改字符串的方式本质上都是返回一个新字符串，而不是直接改变原有字符串，因为字符串一旦赋值是无法修改的。

#### 增：

`'a' + 'b'`，`a${b}`字符串的拼接

str.concat(str1, [...strn])，字符串拼接

#### 删：

subStr(start, [length])：提取子字符串，将要被废弃，尽量不要用。

subString(start, end): 根据开始和结束索引位置截取字符串

slice(start, end): 根据索引截取字符串一部分

#### 查：

charAt(index): 获取字符串对应索引位置的字符，index默认值0，index超出数组长度返回 ' '

indexOf(searchStr): 查找匹配字串，返回对应索引，找不到返回-1

includes(searchStr): 查找匹配子串，找到返回true，找不到返回false

startsWith(searchStr, [position]): 判断字符串是否以子串开头，position用来选择开始位置

endsWith(searchStr, [position]): 判断字串是否以子串结尾，position用来选择结束位置

#### 改：

toLowerCase、toUpperCase： 转大小写

padStart、padEnd(length, padStr): 根据数组长度填充字符串

repeat(times): 复制字符串times次，并返回拼接后的结果

trim、trimLeft、trimRight：删除字符串左、右、左右两边的空格

### 2.转换方法

split：把字符串转换成数组

### 3.模板匹配方法

1.replace(regexp | subString, newString | function)：字符串根据正则匹配，用传入的字符串替换掉匹配的字串。

2.search(regexp)：字符串根据正则匹配，匹配到了返回第一次匹配到的索引，匹配不到则返回-1。

3.match(regexp)：如果正则不是全局匹配，返回一个捕获组，如果全局匹配，返回匹配结果的数组。

## JS中的类型转换机制

Js中类型转换可以分为显式转换和隐式转换

### 显示转换：

Number()

```js
// Number严格转换时严格判断传入的值，只要有一个值无法转换成数组就会返回NaN
let num = Number('123') // 123
let num = Number('123a') // NaN

// 下列的值存在转换
Number({}) // NaN
Number([]) // 0
Number([5]) // 5
Number([1,2,3]) // NaN
Number(true) // 1
Number(false) // 0
Number(undefined) // NaN
Number(null) // 0
```

parseInt()

```js
// parseInt相对Number宽松些，当遇到无法转换的字符后停下来，返回能转换的数字
parseInt('12a3') // 12
```

String()

``` js
// 转换成字符串
String(true) // 'true'
String(undefined) // 'undefined'
String(null) // 'null'
String({a: 1}) // [object Object]
String([1,2,3]) // 1,2,3
```

Boolean()

```
// 转换成布尔值
Boolean([]) // true
Boolean({}) // true
Boolean('') // false
Boolean(undefined) // false
Boolean(null) // false
Boolean(0) // false
Boolean(NaN) // false
Boolean(new Boolean(false)) // false
```

### 隐式转换

发生隐式转换的场景：

四则运算(+ - * /)、比较运算==, >, <、循环语句if，while

#### 自动转换成布尔值：

- undefined
- null
- false
- +0
- -0
- NaN
- ""

上述值会转换成false

#### 自动转换字符串：

在`+`运算中，会出现把非字符串转换成字符串的情况：

```js
5 + '3' = '53'
5 + {} = '5[object Object]'
5 + [] = '5'
5 + [1,2,3] = '51,2,3'
'5' + undefined = "5undefined"
'5' + null = "5null"
```

### 自动转换成数值

除了`+`运算外的其他运算，会把运算子转换成数值：

``` js
'5' - 1 = 4
'5' * '2' = 10
true - 1 = 0
'abc' - 1 = NaN
null + 1 = 1
undefined + 1 = NaN
```

## == 和 ===的区别以及使用场景

== 等于操作符和 === 全等操作符都可以判断等式两边是否相等，但是 == 操作符在比较前会对等式两边进行隐式转换，保证两边类型一致，

转换规则如下：

1.原始值间的比较：string和boolean会转换成number后再比较

2.原始值和引用值的比较：引用值会调用对象valueOf方法转换成原始值后再比较

```js
let obj = {
    valueOf() { return 2 }
}

obj == 2 // ture
```

3.引用值间的比较：比较引用地址值

4.undefined == null 返回true

5.存在NaN比较统一返回false



=== 操作符比较前不会进行类型转换，数据类型不同直接返回false

undefined === null 返回false

#### 用途

一般情况下都用 === 操作符，除了判断对象为空时使用 == 操作符：

```js
if(obj.x == null) {
    // ...doSomething
}

// 等价于
if(obj.x === null || obj.x === undefined) {
    // ...doSomething
}
```



## 深浅拷贝的区别以及如何实现一个深拷贝？

浅拷贝相当于拷贝引用值的第一层，如果属性是原始值，那么拷贝的就是原始值的副本；如果是引用值，那么拷贝的就是引用的地址值。

### 浅拷贝

浅拷贝的实现：

```js
function shallowClone(obj) {
    const newObj = {}
    const keys = Reflect.ownKeys(obj)
    for(let key of keys) {
        newObj[key] = obj[key]
    }
    return newObj
}
```

js中给我们提供了一些可以用于浅拷贝的api：

1.Object.assign(targetObj, ...source)

2.slice()

3.concat

4.拓展运算符...

### 深拷贝

1.引入loadash, 使用_.deepClone()

2.Json.stringify()

3.自己编写递归函数

```js
function deepClone(source, hash = new WeakMap()) {
  if (source == null) return source;
  if (source instanceof Date) return new Date(source);
  if (source instanceof RegExp) return new RegExp(source);
  if (typeof source !== "object") return source;
  if (hash.has(source)) {
    return hash.get(source);
  }
  let cloneObj = new source.constructor();
  hash.set(source, cloneObj);
  let keys = Reflect.ownKeys(source);
  for (let key of keys) {
    cloneObj[key] = deepClone(source[key], hash);
  }
  return cloneObj;
}
```

### 小结：

浅拷贝只拷贝一层，如果要拷贝的对象是嵌套对象，那么拷贝的只是引用地址值，拷贝后的对象和源对象中共用同一份嵌套对象；

深拷贝则是利用递归方式，每一层都重新拷贝，拷贝后的对象和源对象的是不同的引用地址。

## 闭包的理解

### 定义：

一个函数和对其他词法环境的引用绑定在一起，这样的集合体被称为闭包。简单来说，就是内部函数可以访问外部函数的作用域。

### 使用场景

1.维护内部私有变量；

```js
// Counter相当于模块，向外暴露了一些函数api，通过这些api可以改变模块内部的变量
const Counter = function() {
    let _value = 0
    
    return {
        get() {
            return _value
        },
        set(val) {
            _value = val
        },
        increment() {
            _value++
        },
        decrement() {
            _value--
        }
    }
}

// _value变量存在于Counter内部，返回的是暴露的api，无法通过.语法获取到_value，但是可以通过返回的函数获取到_value，实现维护私有变量。
```

2.延长变量生命周期。

函数一般执行完成后弹出执行栈并销毁，但是闭包会形成对当前函数词法环境的引用，即使函数执行环境被销毁，词法环境仍然可以访问，延长了当前函数变量的生命周期。

3.函数柯里化、防抖、节流

```js
// 函数柯里化就是把低阶函数转换成高阶函数，提高代码复用率
function getRectArea (width, height) {
    return width * height
}
// 如果长度固定，仅宽度变化，我们需要每次都手动传入函数
getRectArea(10, 10)
getRectArea(10, 20)
getRectArea(10, 30)

// 函数柯里化后
function getRectArea(width) {
    reutrn (height) => (width * height)
}
// 长度为10的矩形
const getRectWidth10Area = getRectArea(10)
const area1 = getRectWidth10Area(10)
const area1 = getRectWidth10Area(20)
const area1 = getRectWidth10Area(30)
```

```html
// 防抖
<body>
    <button id="btn">Send Message</button>
    <script>
      const btn = document.querySelector("#btn");
      btn.addEventListener("click", bounce(sayHello, 1000));

      function sayHello() {
        console.log("hello world!");
      }

      function bounce(fn, delay) {
        let timer = null;
        return function (...args) {
          console.log(this);
          clearTimeout(timer);
          timer = setTimeout(() => {
            fn.apply(this);
          }, delay);
        };
      }
    </script>
  </body>
```

> 注意：闭包使用后注意解除对闭包的引用，否则GC不会回收这块内存，可能会造成内存泄漏。

## 作用域链的理解？

### 作用域的定义

作用域是指在程序中定义函数和变量时，这些函数和变量能够被访问的范围。

作用域可以区分为：全局作用域（window、global对象）、函数作用域、块级作用域（let const）

### 静态作用域（词法作用域）

js遵循的是静态作用域，也就是在编译阶段我们写好代码之后变量的作用域就已经被确定了：

```js
var a = 2;
function foo(){
    console.log(a)
}
function bar(){
    var a = 3;
    foo();
}
bar() // 2

// 上面的代码可以视为全局作用域中分别包裹了foo作用域和bar作用域，由于foo、bar作用域是同级，他们无法访问彼此间的变量，但是都可以访问到父级全局作用域的变量。
```

### 作用域链

作用域链则是多个作用域嵌套组成，它规定了查找变量的规则。即：内部作用域可以访问外部作用域定义的变量、函数，外部作用域无法访问内部作用域定义的变量、函数（闭包除外）。

## JavaScript的原型和原型链

### 原型

js是基于原型的语言——每个对象都有自己的原型对象。 当访问对象中某个属性时，除了查找当前对象，还会查找对象的原型，对象原型的原型，层层往上搜索，直到找到熟悉or到达原型链末尾。

函数有一个prototype属性，指向函数的原型，原型对象上有constructor属性，指向构造函数；有`__proto__`属性，指向对象原型的原型。

### 原型链

函数有原型，原型有原型的原型，这种层层链接的关系称为原型链。

### 总结：

1.所有对象都继承自Object对象原型，Object对象原型继承根源null；

2.所有函数对象(包括Object对象)，都继承了函数的内置原型，函数内置对象原型继承自对象原型；

3.Function的prototype和`__proto__`属性都继承函数内置的原型；

## JavaScript如何实现继承

### 定义

继承是指在一个类(或对象)的基础上创建一个新的类，新类继承原有类的属性和方法，并且可以在原有类的基础上添加新的属性和方法。继承的有点在于提高代码复用。

js不是真正的OOP语言，它的继承是通过原型链方式去实现的。

### 实现方式

````mermaid
graph TD;
	继承-->不使用Object.create
	不使用Object.create-->构造函数继承
	不使用Object.create-->原型链继承
	构造函数继承-->组合继承
	原型链继承-->组合继承
	组合继承-->寄生组合继承,接近ES6的类继承
	继承-->使用Object.create
	使用Object.create-->原型式继承
	使用Object.create-->寄生式继承
	原型式继承-->寄生组合继承,接近ES6的类继承
	寄生式继承-->寄生组合继承,接近ES6的类继承
````

1.原型链继承：子类原型为父类实例对象

```js
function Parent() {
	this.name = 'niko',
	this.play = [1,2,3]
}
function Child() {
    this.type = 'child'
}
Child.prototype = new Parent()
let c1 = new Child()
let c2 = new Child()
c1.play.pop() // [1,2]
c2.play // [1.2]

// 原型式继承的缺点：所有的子类实例共享同一个父类实例原型，一旦改变父类实例原型的数据，所有子类都被影响
```

2.构造函数继承: 在子类构造函数中调用父类构造函数

```js
function Parent () {
    this.name = 'parent'
}
Parent.prototype.getName = function () {
    return this.name
}

function Child() {
    Parent.call(this)
    this.type = 'child'
}

let c = new Child()
c // Child {name: 'parent1', type: 'child'}

// 构造函数继承的优缺点：
// 优点：子类实例的原型不再互相干扰
// 缺点：只能继承父类的属性和方法，不能继承父类原型的方法
```

把原型链和构造函数继承组合在一起，称为组合式继承：

```js
function Parent() {
  this.pName = "parent";
}

Parent.prototype.getName = function () {
    return this.pName
}

function Child() {
    // 构造函数继承
    Parent.call(this)
    this.cName = 'child'
}

// 原型链继承
Child.prototype = new Parent()
Child.prototype.constructor = Child

let c = new Child()

// 优点：
// 解决了构造函数继承中无法访问父类原型方法的问题
// 缺点：
// 父类构造函数调用了两次，在子类实例和父类原型都有一样的属性冗余
```

3.原型式继承

```js
// 利用Object.create()
let parent = {
    name: "parent",
    friends: ["p1", "p2", "p3"],
    getName: function() {
      return this.name;
    }
 };

let person1 = Object.create(parent)
person1.name = "tom";
person1.friends.push("jerry");
let person2 = Object.create(parent);
person2.friends.push("lucy");
console.log(person1.friends); // ["p1", "p2", "p3","jerry","lucy"]
console.log(person2.friends); // ["p1", "p2", "p3","jerry","lucy"]

// 缺点：
// Object.create是浅拷贝，多个子类实例使用的是同一个父类原型，父类属性修改会影响到所有子类
```

4.寄生式继承

```js
// 寄生式继承本质上和原型式继承是一样的，只不过是给返回的对象添加了一些功能
let parent5 = {
    name: "parent5",
    friends: ["p1", "p2", "p3"],
    getName: function() {
        return this.name;
    }
};

function clone(original) {
    let clone = Object.create(original);
    // 给clone添加了getFriends函数
    clone.getFriends = function() {
        return this.friends;
    };
    return clone;
}

let person5 = clone(parent5);

console.log(person5.getName()); // parent5
console.log(person5.getFriends()); // ["p1", "p2", "p3"]
```

5.寄生组合继承

```js
// 寄生组合继承集成了原型链、构造函数、原型式继承的全部要素
function Parent() {
  this.pName = "parent";
}
// 原型链挂上Parent父类独有方法
Parent.prototype.getpName = function () {
  return this.pName;
};

// 把child的原型指向一个新原型，这个新原型的原型是Parent的原型
function clone(parent, child) {
  child.prototype = Object.create(parent.prototype);
  child.prototype.constructor = child;
}

function Child() {
  // Parent构造函数初始化子类实例
  Parent.call(this);
  this.cName = "child";
}

clone(Parent, Child);
// 原型链挂上Child子类独有方法
Child.prototype.getcName = function () {
  return this.cName;
};

let c = new Child()
console.log(c.getcName())  // child
console.log(c.getpName())  // parent
```

## 谈谈你对this的理解

this是一个关键字，只能在函数内部使用，在函数执行时指向调用它的对象。

### 绑定规则：

1.显式绑定；

``` js
// 利用bind、call、apply显式的修改函数调用时的this指向
function Person() {
    return this.name
}

let obj1 = {
    name: 'niko'
}

let obj2 = {
    name: 'kennys'
}

Person.bind(obj1)() // 'niko'
Person.call(obj2)   // 'kennys'
Person.apply(obj1)  // 'niko'
```

2.隐式绑定；

```js
// 1.函数作为对象上的属性被调用，this指向这个对象
let obj = {
    a: 'niko',
    b: function () {
        return this.a
    }
}

obj.b() // niko

// 2.嵌套对象内的方法，this指向它上一级的对象
let obj = {
    a: 'niko',
    b: {
        a: 'haha',
        d: function () {
            return this.a
        }
    }
}

obj.b.d() // haha

// 3.对象内的方法被赋值给其他变量后，调用时this指向会变化
let obj = {
    a: 'niko',
    b: {
        a: 'haha',
        d: function () {
            return this.a
        }
    }
}

let fn = obj.b.d
fn()  // undefined
```

3.new绑定；

```js
// 1.new 关键字会把this指向函数返回的实例对象
function Person () {
    this.name = 'niko'
}
// 按照前面隐式绑定的规则，函数是在window对象内执行，this指向window(非严格模式下)
let obj = new Person()
// 实际this指向的其实是调用构造函数返回的那个对象
obj.name // 'niko'

// 2.构造函数有return返回一个对象，this指向那个返回的对象
function Person () {
    this.name = 'niko'
    return {
        name: "lory"
    }
}
let obj = new Person()
obj.name // 'lory'

// 3.如果返回的不是对象而是原始值，this指向实例对象
function Person () {
    this.name = 'niko'
    return 1
}
let obj = new Person()
obj.name // 'niko'
```

4.默认绑定。

```js
var name = 'niko'
function person () {
    return this.name
}
person() // niko

// person 是在全局window对象调用，this指向window对象；严格模式下，指向全局对象的this会被绑定为undefined.
```

### 绑定优先级

1.显式绑定 > 隐式绑定

```js
function foo () {
    return this.a
}

let obj1 = { a:2, foo }
let obj2 = { a:3, foo }

// 隐式绑定默认指向调用他们的对象
obj1.foo() // 2
obj2.foo() // 3

// 显式修改绑定后，本应该指向他们对应对象的值，但是现在返回的结果刚好相反
obj1.foo.call(obj2) // 3
obj2.foo.call(obj1) // 2
```

2.new绑定 > 隐式绑定

```js
function foo(val) {
    return this.a = val
}

let obj = {
    a: 1,
    foo
}

obj.foo(3) // 3
let bar = new obj.foo(5)
// new后生成新的实例，this指向新实例，obj是另一个对象，两者值互不相同。说明new的优先级比obj高
obj.a = 3
bar.a = 5
```

3.new和显式绑定

```js
function foo (val) {
    this.a = val
}

let obj = {
    a: 0,
    foo
}

// 把foo函数绑到obj上
let bar = foo.bind(obj)
bar(2)
obj.a // 2
// 把硬绑定到obj的函数当构造函数使用
let baz = new bar(5)
baz.a // 5
obj.a // 2

// 理论上我们已经显式绑定foo到obj上了，new实例时obj.a应该变为5，实际上并没有变，而是new改变了this指向，指向了一个新的实例
```

综上所述：new绑定 > 显式绑定 > 隐式绑定 > 默认绑定

### 箭头函数

箭头函数的this和普通函数不同，他是在定义的时候就确定了，而不是运行时确定。

```js
const foo = () => {
    return this.a
}

let obj = {
    a: 0,
    foo
}

// foo中的this指向window全局对象
obj.foo() // undefined
```

## JavaScript中执行上下文和执行栈

### 执行上下文：

js中执行上下文是对js代码执行环境的抽象概念，只要js代码执行，他就一定处在运行在执行环境中。

执行上下文的分类：

1.全局执行上下文：只有一个，在浏览器中全局对象值得就是window对象。；

2.函数执行上下文：可以有无数个，当函数执行时就会创建新的函数执行上下文，创建私有作用域，函数内部声明的变量无法被外界所用。；

3.eval函数执行上下文：和函数执行上下文同理，但是建议不用eval函数。

### 声明周期

执行上下文的生命周期为：创建阶段——执行阶段——回收阶段

#### 创建阶段

创建阶段指函数被调用，但未执行任何函数内部代码之前

创建阶段行为：

1.创建词法环境：词法环境分为全局环境和函数环境，全局环境的外部环境引用为null，函数环境则包含外部环境引用，这个外部环境可以是全局环境或者是外部函数环境。用户在函数内定义的变量都存放在环境记录中。

词法环境伪代码如下：

```js
GlobalExectionContext = {  // 全局执行上下文
  LexicalEnvironment: {       // 词法环境
    EnvironmentRecord: {     // 环境记录
      Type: "Object",           // 全局环境
      // 标识符绑定在这里 
      outer: <null>           // 对外部环境的引用
  }  
}

FunctionExectionContext = { // 函数执行上下文
  LexicalEnvironment: {     // 词法环境
    EnvironmentRecord: {    // 环境记录
      Type: "Declarative",      // 函数环境
      // 标识符绑定在这里      // 对外部环境的引用
      outer: <Global or outer function environment reference>  
  }  
}
```

2.创建变量环境：变量环境其实也是词法环境的一种，区别在于前者存储函数声明和let、const变量的绑定，后者用于存储变量var的绑定。

例如：

```js
let a = 20;  
const b = 30;  
var c;

function multiply(e, f) {  
 var g = 20;  
 return e * f * g;  
}

c = multiply(20, 30);
```

上述的代码执行上下文如下：

```js
GlobalExectionContext = {

  ThisBinding: <Global Object>,

  LexicalEnvironment: {  // 词法环境
    EnvironmentRecord: {  
      Type: "Object",  
      // 标识符绑定在这里  
      a: < uninitialized >,  
      b: < uninitialized >,  
      multiply: < func >  
    }  
    outer: <null>  
  },

  VariableEnvironment: {  // 变量环境
    EnvironmentRecord: {  
      Type: "Object",  
      // 标识符绑定在这里  
      c: undefined,  
    }  
    outer: <null>  
  }  
}

FunctionExectionContext = {  
   
  ThisBinding: <Global Object>,

  LexicalEnvironment: {  
    EnvironmentRecord: {  
      Type: "Declarative",  
      // 标识符绑定在这里  
      Arguments: {0: 20, 1: 30, length: 2},  
    },  
    outer: <GlobalLexicalEnvironment>  
  },

  VariableEnvironment: {  
    EnvironmentRecord: {  
      Type: "Declarative",  
      // 标识符绑定在这里  
      g: undefined  
    },  
    outer: <GlobalLexicalEnvironment>  
  }  
}
```

可以看到，let、const声明的变量在创建阶段为uninitialized未初始化，而var生命的变量创建阶段就为undefined。

这是因为，创建阶段，会在代码中扫描变量和函数声明，然后将函数声明存储在环境中

但变量会被初始化为`undefined`(`var`声明的情况下)和保持`uninitialized`(未初始化状态)(使用`let`和`const`声明的情况下)

这就是变量提升的实际原因。

3.确定this的指向。

```js
ExecutionContext = {  
  ThisBinding = <this value>,     // 确定this 
  LexicalEnvironment = { ... },   // 词法环境
  VariableEnvironment = { ... },  // 变量环境
}
```

#### 执行阶段

该阶段主要执行变量赋值、代码执行，如果js在代码执行中找不到变量的值，那么就分配为undefined。

#### 回收阶段

等待js引擎回收执行环境。

### 执行栈

js代码在执行过程会创建一个调用栈，存储代码执行时创建的执行上下文，是一个LIFO结构。

js引擎在执行第一行代码时，就会在调用栈中压入全局执行上下文。之后每遇到一次函数执行，都会给调用栈压入一个函数执行上下文，引擎会从栈顶到栈底按循序执行上下文，执行完后的上下文被移出调用栈。

## 说说js中的事件模型

事件模型是W3C指定的一套标准规范，用来处理HTML、XML文档中的事件。

### 事件和事件流

事件是一种机制，处理用户和浏览器之间的交互，例如鼠标点击、键盘输入、页面滚动等。

js中的事件模型是基于DOM的，DOM是一个树结构，在绑定事件时会存在节点触发的先后顺序，这就涉及到事件流的概念。

事件流就是指事件触发的先后循序。

举一个简单的例子：一张纸上有多个同心圆，当你的手指处于圆心时，你不仅处于最内侧圆的圆心，而是所有圆的圆心。实际开发中，如果我们点击了页面某个按钮，我们不光点击了这个按钮，还点击了按钮的容器以及页面，那这个点击必然要有一个先后顺序，这个先后触发顺序就是我们所指的**事件流**。

事件流分为：事件捕获(网景)、事件冒泡(IE)、DOM事件流（结合两者），现代浏览器基本采用DOM事件流。

DOM事件流分为三个阶段：事件捕获、到达节点、事件冒泡，捕获阶段相当于从根节点向下传播，冒泡阶段相当于从目标节点向上传播。

### 事件处理程序

响应事件而调用的函数称为事件处理程序，常见的事件处理程序有:

1.HTML事件处理程序；

HTML中元素对象默认有一些属性(onclick，onkeyup，onscroll等)可以用来指定事件处理程序，但是这种事件模型不够灵活。有以下几个问题：

```js
// 1.同类事件只能绑定一次，后面的绑定会覆盖掉之前的
<input id="btn" type="button" value="Click Me" onclick="showMessage()" />
<script>
  function showMessage() {
    console.log("hello world");
  }

  let btn = document.querySelector('#btn')
  btn.onclick = function() {
    console.log('wa ha ha')
  }
</script>
// 上面代码点击后返回'wa ha ha'

// 2.执行先后顺序导致交互失效，还是拿1的例子，js是单线程，解析document是一行一行执行，上面的input标签解析时，showMessage相关代码还没完成，点击后没有反应 (不会报错时因为大多数html标签对事件处理程序做了try/catch静默失败处理)

// 3.无法实现事件委托和冒泡
```

2.DOM0事件处理程序：就是在js中用代码获取元素、动态添加、删除事件处理程序，例如：

element.onclick = function() { ...todoSomething }，缺点同样是无法实现事件委托和事件冒泡。

3.DOM2事件处理程序（标准事件模型）。

该事件模型有三个阶段：

- 事件捕获阶段：事件从`document`一直向下传播到目标元素, 依次检查经过的节点是否绑定了事件监听函数，如果有则执行
- 事件处理阶段：事件到达目标元素, 触发目标元素的监听函数
- 事件冒泡阶段：事件从目标元素冒泡到`document`, 依次检查经过的节点是否绑定了事件监听函数，如果有则执行

允许我们使用addEventListener()和removeEventListener()方法来动态添加和删除事件处理程序。

事件绑定监听函数的方式如下:

```text
addEventListener(eventType, handler, useCapture)
```

事件移除监听函数的方式如下:

```text
removeEventListener(eventType, handler, useCapture)
```

参数如下：

- `eventType`指定事件类型(不要加on)
- `handler`是事件处理函数
- `useCapture`是一个`boolean`用于指定是否在捕获阶段进行处理，一般设置为`false`与IE浏览器保持一致

4.IE事件处理程序(IE8后废弃)

## typeof和instanceof的区别

typeof操作符接受一个操作数，返回一个字符串，表明操作数的类型。

```js
// 1.常规
typeof 5 // number 
typeof '5' // string
typeof true // boolean
typeof Symbole() // 'symbol'
typeof undefined // 'undefined'

// 2.特例
typeof function () {} // 'function'
typeof null // 'object'

// 通常typeof可以判断原始值的类型，但是对于null，虽然是原始值，但是null通常用于表示空对象的引用，所以返回'object'，这算是一个js的历史包袱。
```

instanceof操作符判断构造函数的prototype原型在不在某个实例对象的原型链中。

```js
object instanceof constructor

// 1.用instanceof判断原始值，统一返回false
let str1 = 'hello'
let str2 = new String('world')
str1 instanceof String // false
str2 instanceof String // true

// 2.instanceof实现原理
function myInstanceof (left, right) {
  // 传入的对象不是引用类型 or 传入对象为空
  if(typeof left !== 'object' || left == null) return false
  let proto = Object.getPrototypeOf(left)
  while(true) {
    if(proto == null) return false
    if(proto === right.prototype) return true
    // 查找原型的原型
    proto = Object.getPrototypeOf(proto)
  }
}
```

二者区别：

1.typeof返回变量类型，instanceof返回布尔值；

2.typeof能够判断基本数据类型，但是没法区分引用数据类型(null、function除外)；

3.instanceof则相反，它能够区分引用类型，但是没法区分基本数据类型。



Object.prototype.toString.call()可以通用检测数据类型，例如：

```js
Object.prototype.toString.call('5') // '[object String]'
Object.prototype.toString.call(new Set()) // '[object Set]'
```

可以根据实际情况封装一个通用的类型判断：

```js
function getType(val) {
  let type = typeof val;
  // val是原始值
  if (type !== "object") return type;
  // val是引用值
  return Object.prototype.toString.call(val).replace(/^\[object (\S+)\]$/, '$1');
}
```

## 事件代理及其应用场景

### 定义：

事件代理就是把一个元素响应事件函数委托给另一个函数。

事件流分为：捕获阶段、目标阶段、冒泡阶段。事件委托就是发生在冒泡阶段的。

事件委托就是把一组元素的事件委托到父元素or更外层元素上，绑定事件的是外层元素，而不是目标元素。

当目标元素事件响应时，会通过冒泡机制触发绑定到外层元素的事件上，在外层元素执行事件处理函数。

### 应用场景：

列表、表格中存在大量子列表项时使用，下面是一个例子：

```html
<ul id="list">
  <li>item 1</li>
  <li>item 2</li>
  <li>item 3</li>
  ......
  <li>item n</li>
</ul>
```

如果给每个li绑定处理函数，绑定开销大，内存消耗大

```js
// 获取目标元素
const lis = document.getElementsByTagName("li")
// 循环遍历绑定事件
for (let i = 0; i < lis.length; i++) {
    lis[i].onclick = function(e){
        console.log(e.target.innerHTML)
    }
}
```

可以把li的事件委托给父元素ul中

```js
// 给父层元素绑定事件
document.getElementById('list').addEventListener('click', function (e) {
    // 兼容性处理
    var event = e || window.event;
    var target = event.target || event.srcElement;
    // 判断是否匹配目标元素
    if (target.nodeName.toLocaleLowerCase === 'li') {
        console.log('the content is: ', target.innerHTML);
    }
});
```

例子2：给一个列表进行增删处理

```js
<body>
    <input type="button" id="btn" value="添加" />
    <ul id="list">
      <li>item1 <button>删除</button></li>
      <li>item2 <button>删除</button></li>
      <li>item3 <button>删除</button></li>
      <li>item4 <button>删除</button></li>
      <li>item5 <button>删除</button></li>
    </ul>
    <script>
      const list = document.querySelector("#list");
      const btn = document.querySelector("#btn");
      let length = document.getElementsByTagName("li").length

      btn.onclick = function (e) {
        let newLi = document.createElement("li");
        newLi.innerHTML = `item${length + 1} <button>删除</button>`;
        length++
        list.appendChild(newLi);
      };

      list.onclick = function (e) {
        const target = e.target.parentNode;
        if(target.nodeName.toLowerCase() === 'li') {
          target.remove();
        }
      };
    </script>
</body>
```

可以看到删除列表子项的事件处理函数绑定在父元素ul中，不需要给每个子项都绑定函数。

### 总结：

委托的两大优点：

1.减少绑定开销，减少内存消耗，提高性能；

2.减少重复工作

局限性：

1.blur，focus事件没有冒泡机制，无法使用事件委托；

2.mousemove、mouseout事件，虽然可以冒泡，但是这些事件是高开销事件，委托的意义不大。

3.事件委托可能会导致不该触发事件的元素触发事件，可以用阻止冒泡阻止事件的误触。

## new操作符具体干了什么？

new操作符创建了构造函数的实例对象，它分为以下几步进行：

1.创建一个新对象；

2.把新对象和构造函数通过原型链联系起来；

3.把构造函数中的this绑定为新对象；

4.执行构造函数，初始化新对象；

5.如果构造函数没有返回值，或者返回值是原始值，那么返回这个新对象；如果构造函数返回一个引用值对象，那么返回这个引用值对象，新创建的对象被废弃。

下面是模拟new的实现：

```js
function myNew(fn, ...args) {
  // 1.创建新对象
  const obj = {};
  // 2.把新对象二点原型和构造函数原型联系起来
  obj.__proto__ = fn.prototype;
  // 3.把构造函数执行时的this指向新对象，并初始化这个新对象
  const result = fn.apply(obj, args);
  // 4.判断构造函数返回值，如果没有返回值or返回值为原始值，则返回新对象；如果返回值是引用值，那就返回这个引用值
  return result instanceof Object ? result : obj;
}
```

可以看到效果一样：

```js
function Person(name, age) {
  this.name = name;
  this.age = age;
}

Person.prototype.speak = function () {
  console.log(this.name + this.age);
};

let p1 = new Person("niko", 18); // Person {name: 'niko', age: 18}
let p2 = myNew(Person, "lala", 22); // Person {name: 'lala', age: 22}

```

## ajax原理与实现

### ajax定义和原理

ajax——async javascript and XML，异步js和XML，可以在不刷新页面的情况下和服务器交换数据，局部刷新页面。

ajax的原理就是利用XMLHttpRequest这个api向服务器发送异步请求，获取服务器数据，之后用js操作DOM实现页面的刷新。

### 实现过程：

1.创建XMLHttpRequest对象；

2.利用XMLHttpRequest对象的open方法初始化请求参数(url，请求方法，请求头等)；

3.利用XMLHttpRequest的send方法和服务器建立连接并向服务器发送请求(send在post方法中可以传入body参数，在get方法中body参数默认为null)；

4.利用XMLHttpRequest的onreadystatechange事件监听与服务端的通信状态；

5.接受并处理服务端返回的数据结果；

6.利用数据重新局部渲染页面。

上面的过程用代码实现如下：

```js
function ajax(options) {
    // XMLHttpRequest对象
    const xhr = new XMLHttpRequest();
    // 请求类型
    let type = (options.type || "GET").toUpperCase();
    let url = options.url;
    let body = options.data;
    if (type === "GET") {
      xhr.open(type, url);
      xhr.send(null);
    } else if (type === "POST") {
      xhr.open(type, url);
      xhr.setRequestHeader("Content-Type", "application/json");
      xhr.send(JSON.stringify(body));
    }

    // 监听返回数据状态
    xhr.onreadystatechange = function () {
      if (xhr.readyState === 4) {
        let status = xhr.status;
        if (status >= 200 || status < 300) {
          options.success && options.success(xhr.response);
        } else {
          options.fail && options.fail(status);
        }
      }
    };
}

let options = {
    type: 'POST',
    data: {
      username: 'admin',
      password: '123456'
    },
    url: 'http://localhost:3000/verify'
}
ajax(options)
```

readyState有五个状态，分别如下：

| 值   | 状态                       | 描述                                 |
| ---- | -------------------------- | ------------------------------------ |
| 0    | UNSEND未打开               | open()还没调用                       |
| 1    | OPENED未发送               | send()还没调用                       |
| 2    | HEADERS_RECEIVED获取响应头 | send()调用，响应头和响应状态已经返回 |
| 3    | LOADING下载响应体          | 响应体下载中                         |
| 4    | DONE请求完成               | 请求完成                             |

## bind、call、apply的区别及其实现

bind、call、apply都能接收参数改变函数执行时this的指向。

使用场景：一些异步操作下（比如计时器、发起请求等），这些异步操作的回调函数都是在全局执行环境中执行，this指向window。

区别：

1.bind、call、apply都能改变this的指向

2.bind、call、apply第一个参数为this指向对象，如果第一个参数是undefined or null，则this默认指向window

3.bind返回改绑this后的函数且不会执行；call、apply返回改绑this后函数的执行结果，改绑后原函数会执行。

4.bind、call接受参数列表，apply接受参数数组；bind可以多次传入参数，apply、call只能一次性传入：

```js
function add (a, b) {
  return a + b
}

let obj = {
}

// 下面两种方式的结果是等价的
let res = add.bind(obj, 1)
res(2)

let res2 = add.bind(obj, 1, 2)
```

### 模拟bind、call、apply的代码实现

1.apply的实现

```js
function myApply(ctx = window, args) {
  // 判断调用myApply函数的是不是一个函数
  if (typeof this !== "function") {
    throw new Error("Type Error");
  }

  // 给指向的对象添加要执行的函数
  const fn = Symbol("fn");
  ctx[fn] = this;

  // 利用了this的隐式绑定，ctx[fn]执行时this指向ctx
  const res = ctx[fn](...args);
  delete ctx[fn];
  return res;
}

Function.prototype.myApply = myApply;

let obj = {};

function add(a, b) {
  return a + b;
}

add.myApply(obj, [1, 2]);
```

2.call的实现思路和apply是一致的，区别就是在于入参是参数列表不是参数数组

```js
function myCall(ctx = window, ...args) {
  if (typeof this !== "function") {
    throw new Error("Type Error");
  }

  const fn = Symbol("fn");
  ctx[fn] = this;

  const res = ctx[fn](...args);
  delete ctx[fn];
  return res;
}

Function.prototype.myCall = myCall;

let obj = {};

function add(a, b) {
  return a + b;
}

add.myCall(obj, 1, 2);
```

3.bind的实现思路

```js
Function.prototype.bind = function (context, ...args) {
  if (typeof this !== "function") {
    throw new Error("Type Error");
  }
  // 保存this的值
  var self = this;

  return function F() {
    // 用new去调用bind修改this后返回的函数
    if (this instanceof F) {
      return new self(...args, ...arguments);
    }
    return self.apply(context, [...args, ...arguments]);
  };
};
```

## 说说你对事件循环的理解

### 定义：

JS是单线程的语言，UI渲染和JS代码执行在同一主线程，这就可能导致阻塞，为了解决单线程阻塞提出的方法就是事件循环。

JS把任务分为同步任务和异步任务，同步任务在主线程中同步进行，异步任务放置在异步队列中。当主线程中的任务执行完成时，会读取异步任务队列中的任务进入主线程中执行，这个循环往复的过程就是我们所述的事件循环。

### 宏任务与微任务：

异步任务分为**宏任务**和**微任务**。

宏任务例如：setTimeout/setTimeInterval、postMessage、MessageChannel、UI Render、NodeJS中的I/O

微任务例如：Promise.then、process.nextTick、queueMicroTask、MutationObserver

总的执行机制如下：

> 主函数执行 —— 执行所有微任务 —— 执行所有宏任务 —— UI渲染 —— ...循环上述

### async 与 await

async await是Promise的语法糖，使得我们可以写同步代码的方式去编写异步代码（本质仍然是微任务队列的异步函数）：

```js
// 传统promise处理异步回调通常要在then方法中进行
function getData() {
    return new Promise((resolve, reject) => {
        setTimeout(() => {
            resolve('done')
        }, 1000)
    })
}

getData().then((res) => {
    console.log(res)
})

// async
async function getData () {
    // 这一步我们可以像同步代码那样，把await的结果赋值给res，await相当于执行了promise.then
    let res = await new Promise(resolve => {
        setTimeout(() => {
            resolve('done')
        }, 1000)
    })
    console.log(res)
}
getData()
```

## DOM的操作

什么是DOM？DOM是HTML、XML文档的标准API，定义了文档逻辑结构和内容在编程语言中的表现形式。并可以通过DOM API去改变文档的结构、样式、内容。HTML、XML文档都可以用DOM表示成一颗节点层级树。

### 增：

1.创建新节点：document.createElement

2.创建文本节点: document.createTextNode

3.创建文档片段: document.createFragment

4.创建属性: document.createAttribute

5.添加节点，把子节点插入父节点中最后的位置：[parent].appendChild(node)

6.添加节点，把子节点查到指定位置：[parent].insertBefore(node, referNode)，node被插入到referNode之前。

7.设置节点属性: [node].setAttribute('className', 'classValue')

### 查：

1.查单个DOM元素：document.querySelector

2.查DOM列表：document.querySelectorAll

### 改：

1.改变DOM节点内html内容：DOM.innerHTML = 'xxx'

2.改变DOM节点内文本内容（传入html结构会被转义）：DOM.innerText = 'xxx'

3.改变DOM节点内属性：DOM.style.fontSize = '12px'（style返回一个样式对象，如果要修改的样式是多词组成，要改成驼峰形式）

### 删：

1.删除父节点中子节点：[parentNode].removeChild(node)，node节点从父节点中删除。

2.从DOM树中删除节点：[node].remove()，node节点将从它所在的DOM中删除。

## 说说对BOM的理解？

1.window：浏览器实例与全局对象，每个新页签有一个单独的window对象

2.location：url的一些相关属性，例如协议、主机名、端口号、hash值、服务器文件路径等等。hash值改变不会引起页面的刷新。

3.history：操作浏览器url历史记录，控制页面前进、后退。

4.navigator：浏览器信息、浏览器类型

5.screen：客户端显示器的一些信息

## 内存泄漏：

### 定义：

由于疏忽、错误导致应用程序未能释放不再使用的内存，导致这块内存之后无法被应用程序重新分配的现象，称为内存泄漏。

### 垃圾回收机制：

JS自带GC回收机制，当满足条件时，触发GC，自动回收不再使用的变量，自动释放其内存。

js常见的垃圾回收机制分为：

1.标记清理：回收时机不确定，无法实时监测不可达对象。

2.引用计数：回收时机确定，但是无法回收循环引用的对象。

## JS本地存储方式

### 方式：

本地缓存通常有四种方式：

#### 1.cookie：

cookie，通常用于网站辨别用户身份而存储在用户本地终端的数据，早期用于解决http无状态问题。它的大小4KB作用，由name-value键值对和控制cookie有效期、安全性、使用范围等属性组成的字符串（例如设置了HttpOnly，cookie就无法被js代码获取，通常用来预防XSS跨站脚本攻击）。

cookie常用属性：

Expires：设置过期时间，格式为格林威治时间，如果为 ‘session’，那么会话关闭后就会被清除。

```js
Expires=Wed, 21 Oct 2015 07:28:00 GMT
```

Max-Age: 设置Cookie失效前经过的秒数（一样是过期时间，但是优先级高于Expires）

```js
Max-Age=604800
```

Domain：指定Cookie送达的主机名

Path: 指定URL路径，该路径出现在请求的资源路径时才可以发送Cookie首部。

例如，如果将Cookie设置在"http://www.example.com/foo/bar/index.html"页面中，那么默认情况下，该Cookie将在"http://www.example.com/foo/bar/"及其子目录下发送，而不会在其他目录下发送。如果需要在其他目录下使用相同的Cookie，则需要显式地设置Cookie的path属性。

HttpOnly：属性如果为true，Cookie将无法被JS代码相关API获取，常用于预防XSS跨站脚本攻击。

Secure：属性为true，那么只有https协议下会携带该Cookie

Cookie的使用方式：

```js
// 设置cookie
document.cookie = '名字=值';

// 关于cookie的修改，首先要确定domain和path属性都是相同的才可以，其中有一个不同得时候都会创建出一个新的cookie
Set-Cookie:name=aa; domain=aa.net; path=/  # 服务端设置
document.cookie =name=bb; domain=aa.net; path=/  # 客户端设置
```

#### 2.localStorage、sessionStorage

二者都是H5标准新方法，IE8以后的浏览器兼容。

特点：

1.持久化存储（localStorage是永久性；sessionStorage是会话性，一旦关闭页面后会被删除）

2.存储容量大约5MB左右

3.存储信息在同域中共享，受同源策略限制

4.对缓存增删改查时，会触发其他标签页的 Web Storage事件（同源状态下），但是不会触发当前页面的Web Storage事件

5.不能像Cookie那样设置过期事件，也不能存储对象，必须先转换成字符串。

API：

getItem获取值

setItem设置值

removeItem删除值

clear清空

#### 3.indexedDB

indexedDB是一种面向对象数据库，和传统关系型数据库不一样，使用键值存储形式而不是行列表。可以用来存储客户端大量结构化数据（文件、blobs）

特点：

1.是一个数据库，数据库的功能都有。

2.存储理论上没有上限，chrome默认上限为磁盘容量的50%。

3.所有操作都是异步的。

4.原生支持存储JS对象。

#### 4.异同：

1.存储大小：cookie大小4kb，local、session大小5MB

2.有效时间：local永久，session会话，cookie通过expires或max-age控制

3.与服务器交互形式：cookie请求时

#### 5.使用情景：

1.标记、跟踪用户行为，用cookie

2.长期保存本地的数据（令牌），用localStorage

3.敏感信息、单次登录用sessionStorage

4.大数据量、在线文档保存编辑历史，用indexedDB

## 说说你对函数式编程的理解

### 定义：

函数式编程和面向对象编程都是编程范式。

面向对象编程通常基于`类`对象的思想设计程序。类是一个封装了数据和方法的实体，通过数据传递进行交互。OOP的核心在于如何组织代码，实现更好的类封装。

函数式编程则是基于函数的思想来设计程序。函数就是将输入转换成输出的映射关系，通常是无状态、无副作用的（所谓的纯函数），不会改变程序的状态。我们通过将一系列函数通过某种组合来实现程序的功能（类似于拼积木）。

主要区别如下：

1. 数据和行为的组织方式不同。OOP将数据和行为封装在对象中，FP则将它们视为独立的输入和输出。
2. 对象通常具有状态，可以改变它们的内部状态，而函数通常是无状态的，即它们不会改变任何数据或状态。
3. OOP强调继承、多态和封装等概念，而FP则强调纯函数、高阶函数和不可变性等概念。
4. OOP通常使用类和对象来组织程序，而FP通常使用函数和数据结构来组织程序。
5. OOP通常更适合处理复杂的对象和关系，而FP则更适合处理简单的操作和计算过程。

需要注意的是，这两种编程范式并不是互斥的，它们可以互相补充和结合使用，比如在Java 8及以上版本中，就支持将函数式编程的元素引入到面向对象编程中。

### 纯函数：

纯函数 = 无状态、数据不可变的函数。所谓的无状态，指的是函数无论在什么环境下执行，只要入参不变，结果就不变。数据不可变指的是，函数执行过程中，函数内部数据、状态不会发生任何变化。

### 高阶函数：

一个函数A的返回值是另一个函数B，那么这个函数A就被称为高阶函数。

### 柯里化：

把一个多入参函数改成嵌套的一元函数，本质上柯里化就是将函数转变成高阶函数。

特点：

1.纯函数更纯，每次接收一个入参，松散解耦

2.惰性执行

### 组合与管道

```js
function A(val) {
  return val * 3;
}

function B(val) {
  return val + 2;
}

// 管道 从左往右
const pipe =
  (...fns) =>
  (val) =>
    fns.reduce((acc, fn) => fn(acc), val);

// 组合 从右往左
const compose = (...fns) => {
  const reverseFns = fns.reverse();
  return (val) => reverseFns.reduce((acc, fn) => fn(acc), val);
};

let p = pipe(A, B);
let c = compose(A, B);

p(1);
c(1);
```

函数式编程的优点：

1.状态管理更方便：函数式编程宗旨就是无状态或少状态，减少由于状态异常引起的错误。

2.代码复用方便：由于函数式编程追求纯函数，无状态 + 无副作用使得它再任何条件下执行都能得到一样的结果，复用时可以忽略内部实现。

3.组合优雅：网页可以是多个组件组成，同理大函数可以是多个小函数组成，复用性更强。

4.更好的单元测试：因为纯函数的特性，使得单元测试共容易。

缺点：

1.性能：由于函数式编程追求组合，大函数由小函数组成，小函数由更小函数组成，可能会造成过度封装以及执行时作用栈的切换开销；

2.内存消耗更大：函数执行会进入调用栈，并创建一个局部对象维护不可变数据，这使得内存开销增大。

3.递归算法来处理大型数据集可能会导致栈溢出或性能问题。

## js中的函数缓存

### 定义

函数缓存就是把函数的运行结果进行缓存，减少重复运算的开销。js中实现函数缓存的实现利用了函数闭包、高阶函数、柯里化。

```js
function memorize(func, context) {
  const cache = Object.create(null);
  // 存储当前this
  context = context || this;
  return (...args) => {
    // 判断缓存对象中是否已经记录有对应的计算结果
    if (!cache[args]) {
      cache[args] = func.apply(context, args);
    }
    return cache[args];
  };
}

function add(a, b) {
  return a + b;
}

let m = memorize(add)
m(100, 200) // 300，并把结果记录缓存
m(100, 200) // 300，不计算，直接取缓存
```

### 应用场景

1.对于执行复杂计算函数，可以缓存计算结果。

2.保存纯函数计算结果。

3.有重复值的递归函数。

## 为什么0.1 + 0.2 === 0.3返回false

这是因为十进制转换二进制是精度丢失造成的问题。

根据IEEE 754标准，js的number类型实际上是一个双浮点数，它由64个比特组成：

1.符号位：第一比特位用来判断正负，0代表正数，1代表负数。

2.指数位：2~12比特位，总共11位用来保存指数，可以表示范围为2^-1024 ~ 2^1023。

3.尾数位：剩下的52位用来存储二进制数，超出的部分将会被截断并进1舍0。

0.1和0.2转换成二进制后是无限不循环小数，会被阶段，造成精度损失（类似于十进制中 1 / 0.3）。

计算机存储双精度浮点数需要先把十进制数转换为二进制的科学记数法的形式，然后计算机以自己的规则{符号位+(指数位+指数偏移量的二进制)+小数部分}存储二进制的科学记数法

因为存储时有位数限制（64位），并且某些十进制的浮点数在转换为二进制数时会出现无限循环，会造成二进制的舍入操作(0舍1入)，当再转换为十进制时就造成了计算误差

解决方案：

1.小数整数化处理（fix point），把0.1 + 0.2转换成 (1 + 2) / 10，把小数运算转换成整数运算，从而解决误差问题。

2.用toPrecision凑整后用parseFloat转换成数字展示

```js
parseFloat(1.4000000000000001.toPrecision(12)) === 1.4
```

3.不用等于而是用一个范围去判断

```js
0.1 + 0.2 === 0.3 // false

Math.abs((0.1 + 0.2) - 0.3) < 1e-6 // true
```

## 防抖与节流

防抖：n秒后执行事件，如果在n秒内重复触发，计时重置

节流：n秒后执行事件，如果在n秒内重复触发，只有一次生效

防抖和节流可以形象描述成回城和传送。回城可以重复操作，下一次回城会打断上一次回城；节流相当于使用了tp，tp这一过程有读秒，读秒内重复tp这个操作是不会中断执行。

通常用来减少函数、事件的触发频率。

代码实现：

```js
function debounce(fn, layout) {
  let timer = null;
  return (...args) => {
    clearTimeout(timer);
    timer = setTimeout(() => {
      fn.apply(this, args);
    }, layout);
  };
}

function throttle1(fn, delay) {
  let timer = null;
  return (...args) => {
    if (!timer) {
      timer = setTimeout(() => {
        fn.apply(this, args);
        timer = null
      }, delay);
    }
  };
}

function throttle2(fn, delay) {
  let prevTime = null;
  return (...args) => {
    let nowTime = Date.now();
    if (nowTime - prevTime < delay) return;
    fn.apply(this, args);
    prevTime = nowTime;
  };
}
```

应用场景：

防抖：

1.用户输入框，用户输入完后再发送请求

2.手机号、邮箱检验；

3.获取窗口大小resize，调整结束后再计算窗口大小

节流：

1.搜索联想功能

2.滚动加载

## 判断一个元素是否在可见区域？

判断一个元素是否在可见区，有三种方法：

1.offset + scrollTop

```js
function isInViewPortOfOne (el) {
    // viewPortHeight 兼容所有浏览器写法
    const viewPortHeight = window.innerHeight || document.documentElement.clientHeight || document.body.clientHeight 
    const offsetTop = el.offsetTop
    const scrollTop = document.documentElement.scrollTop
    const top = offsetTop - scrollTop
    return top <= viewPortHeight
}
```

2.getBoundingClientRect：该方法会获得元素的一个对象，对象包含了元素的长、宽以及元素相对于视口的属性left、right、bottom、top

```js
function isInViewPort(element) {
  const viewWidth = window.innerWidth || document.documentElement.clientWidth;
  const viewHeight = window.innerHeight || document.documentElement.clientHeight;
  const {
    top,
    right,
    bottom,
    left,
  } = element.getBoundingClientRect();

  return (
    top >= 0 &&
    left >= 0 &&
    right <= viewWidth &&
    bottom <= viewHeight
  );
}
```

3.intersection Observer：重叠观察者，判断两个元素是否重叠。

