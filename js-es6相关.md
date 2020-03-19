## JS方面foo

`备注： + 代表被问到的次数，没有 + 代表自己整理了，但没被问到`

#### 1.js继承的方式+

1. 原型链继承
2. 借用构造函数继承（通过call()实现）
3. 组合继承(原型+借用构造)
4. 通过ES6中class的extends关键字实现继承



#### 2.NEW操作符做了那些事情+

1. 创建一个新对象；
2. 将构造函数的作用域赋给新对象（因此this就指向了这个新对象）；
3. 执行构造函数中的代码（为这个新对象添加属性）；
4. 返回新对象



#### 3.call/aplay的区别++

​	作用：动态改变某个类的某个方法的运行环境（执行上下文）

- call可以传入多个参数；
- apply只能传入两个参数，所以其第二个参数往往是作为数组形式传入



#### 4.this指向哪里？+

​	JavaScript this 关键词指的是它所属的对象。

​	它拥有不同的值，具体取决于它的使用位置：

- 在方法中，this 指的是所有者对象。
- 单独的情况下，this 指的是全局对象。
- 在函数中，this 指的是全局对象。
- 在函数中，严格模式下，this 是 undefined。
- 在事件中，this 指的是接收事件的元素。

像 call() 和 apply() 这样的方法可以将 this 引用到任何对象。



#### 5.闭包的理解和优缺点+

- 能够读取其他函数内部变量的函数/定义在一个函数内部的函数；
- 闭包的作用是可以创建封闭作用域
- 闭包的优点：可以避免全局变量的污染
- 闭包的缺点：常驻内存，会增大内存使用量，使用不当很容易造成内存泄露



#### 6.防抖和节流的使用场景+

debounce （防抖）函数防抖在执行目标方法时，会等待一段时间。当又执行相同方法时，若前一个定时任务未执行完，则 clear 掉定时任务，重新定时。

- search搜索联想，用户在不断输入值时，用防抖来节约请求资源。
- window触发resize的时候，不断的调整浏览器窗口大小会不断的触发这个事件，用防抖来让其只触发一次

```javascript
const _.debounce = (func, wait) => {
    let timer;

    return () => {
        clearTimeout(timer);
        timer = setTimeout(func, wait);
    };
};
```



throttle （节流）是为了限制函数一段时间内只能执行一次，在延时的时间内，方法若被触发，则直接退出方法

- 鼠标不断点击触发，mousedown(单位时间内只触发一次)
- 监听滚动事件，比如是否滑到底部自动加载更多，用throttle来判断

```javascript
const _.throttle = (func, wait) => {
    let timer;
    return () => {
        if (timer) {
            return;
        }

        timer = setTimeout(() => {
            func();
            timer = null;
        }, wait);
    };
};
```



#### 7.浏览器的事件触发+

冒泡和捕获，事件流，捕获 => 目标阶段 => 冒泡

addEventListener('click',function(){},false)  冒泡阶段触发

addEventListener('click',function(){},true)  捕获阶段触发

长列表场景：事件代理，将事件绑定到父元素，通过冒泡将其冒到父元素上进行处理，target属性用来区分那个子元素.优点，节省内存，不用为新增元素绑定事件。

阻止冒泡：stopPropagation()



#### 8.== 和 === 的区别+

​	==， 两边值类型不同的时候，要先进行类型转换，再比较。
​	===，不做类型转换，类型不同的一定不等。



#### 	9.数组去重排序+

​	数组去重：

```javascript
function unique (arr) {
  return Array.from(new Set(arr))
}
```

​	数组排序：function cmp(a,b){return a-b};     array.sort(cmp);



#### 10.浅拷贝与深拷贝++

​	浅拷贝： =号符/Array.prototype.slice() — 数组/Object.assign() — 对象

​	深拷贝：JSON.parse(JSON.stringify());

```javascript
//递归实现
function isObj(obj) {
    return (typeof obj === 'object' || typeof obj === 'function') && obj !== null
}
function deepCopy(obj) {
    let tempObj = Array.isArray(obj) ? [] : {}
    for(let key in obj) {
        tempObj[key] = isObj(obj[key]) ? deepCopy(obj[key]) : obj[key]
    }
    return tempObj
}
```



#### 11.判断一个对象是不是promise+

```javascript
function isPromise(e){
  return !!e&&typeof e.then=="function"
}
```



#### 12.事件队列+

- 整体`script` 作为第一个宏任务进入主线程。
- 遇到`setTimeout`，其回调函数被分发到宏任务Event Queue中。
- 遇到`Promise`，new Promise直接执行，输出Promise。then被分发到微任务Event Queue中。
- 遇到console.log，立即执行，输出。
- 整体代码`script`作为第一个宏任务执行结束，看看有哪些微任务？我们发现了`then`在微任务Event Queue里面，执行。
- ok，第一轮事件循环结束了，我们开始第二轮循环，当然要从宏任务Event Queue开始。我们发现了宏任务Event Queue中`setTimeout`对应的回调函数，立即执行。
- 所有代码结束。



#### 13.内置类型

* null
* undefind
* 布尔值
* 数字
* 字符串
* 对象
* symbol



#### 14.原型链

​		当访问对象中的属性或方法时，如果对象中没有该属性或方法，则会向此对象的 __proto__ 寻找该属性或方法，如果找了，就返回该属性，若没有找到，则继续向此对象的 __proto__ .__proto__ 查找该属性,一直访问的windows对象，都没有返回undefind

- 在任何对象上查找某个属性时，会先在其自身上找，当查找不到时，会在此对象的 __proto__ 属性上去查找
- 可以用 Object.create(p) 创建一个 __proto__ 为 p 的对象，即返回的对象的 __proto__ 指向 p
- 可以通过 Object.getPrototypeOf(obj) 获得 obj 对象的【__proto__】
  - 其与对象的 __proto__ 属性其实是同一个东西，只是后者更加标准
  - 但在更早的浏览器中，这两者都是不可用的
- 可以通过Object.setPrototypeOf(obj1, obj2)设置obj1对象的__proto__为obj2



#### 15.JS里有那些异步处理的方法

* 回调函数
* 事件监听
* 发布/订阅
* Promises对象



#### 16.浏览器新增的异步请求方式？跨域参数

​	fetch  调用时不会带cookie

​	mode: 'cors',



#### 17.模块化规范

Commonjs、amd、cmd



#### 18.es6扩展运算符使用场景

 * 数据连接、合并
 * 替换apply方法，一般在函数调用时处理参数
 * 数组对象的拷贝
 * 字符串转数组



#### 19.箭头函数的特点和使用场景

​	特点：

 * 箭头函数会捕获其所在父执行上下文的`this`值，作为自己的`this`值；

 * 箭头函数不能作为构造函数，和 new 一起用就会抛出错误；

 * 箭头函数没有原型属性

   使用场景：在任何需要绑定 `this` 到父执行上下文，而不是函数本身时，箭头函数十分适用。



#### 20.import/export和require有什么区别？

是语法层级的

方便静态分析和优化



#### 21.如何判断一个变量是不是数组

​	现在： Array.isArray()

​	以前： Object.toString.call(val) == '[object Array]'



#### 22.类数组对象怎么转换为数组

​	Array.from(arrayLike)

​	Array.prototype.slice.call(arrayLike)



#### 23.for...in 和 Object.keys的区别

​	for...in 会遍历所有可枚举属性

​	Object.keys 返回自有可枚举属性组成的数组



#### 24.纯函数的特点及其好处

特点：相同输入，永远得到相同输出

好处：没有副作用，可测试性



## ES6相关

#### 1.let/const ++

​	let不会提升

​	const设置的原始值是不可以改变，但设置的对象内的属性值是可以改变的



#### 2.async/await ++

​	是生成器函数的语法糖  es7出现的  返回promise



#### 3.promise++

​	有3个状态，进行中，已完成，已失败    /  特点：一旦状态改变就不会在变



#### 4.``模版字符串，里面可以写变量+



#### 5.介绍class和ES5的类以及区别 +

​	必须new

​	原型上的方法自动不可枚举

​	继承时必须调用super



#### 6.for in 和 for of 区别 +

​	for of 循环的是数组/字符串的值，不能循环普通对象/遍历 **可迭代对象（iterable object）** 定义的可迭代的数据 ，比如遍历 Array，Map，Set，String，TypedArray，arguments 等对象的数据。

​	for in 循环的是数组/字符串/对象的下标或key  循环对象及其原型上的可枚举属性/以任意顺序遍历对象的**可枚举属性 （enumerable properties）**，包括对象从其构造函数原型中继承的属性。

​	如何使对象可以使用for of

```javascript
newObj[Symbol.iterator] = function* (){
    let keys = Object.keys( this )
    
    for(let i = 0, l = keys.length; i < l; i++){
        yield this[keys[i]]
    }
}
```



#### 7.ES6关于数组的一些处理 +++

* map对数组各个元素调用指定函数，并返回新数组
* filter过滤出满足条件的元素
* reduce将数组中所有的元素迭代出一个值
* find查找一个符合条件的元素
* slice() 返回数组的一部分
* splice() 插入、删除或替换数组元素

pop/push/shift/unshift会改变原数组



#### 8.ES6关于对象的一些处理+

* object.assign()



#### 9.劫持，代理proxy



#### 10.装饰器

​	@符号
