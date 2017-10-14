<!-- @import "[TOC]" {cmd="toc" depthFrom=1 depthTo=6 orderedList=false} -->
<!-- code_chunk_output -->

* [HTML](#html)
* [CSS](#css)
* [JavaScript](#javascript)
	* [V8， node的历史，npm的诞生](#v8-node的历史npm的诞生)
	* [DOM、 BOM](#dom-bom)
			* [`window.onload` 和 `DOMContentLoaded`](#windowonload-和-domcontentloaded)
	* [基本类型 和 引用类型](#基本类型-和-引用类型)
			* [基本类型](#基本类型)
			* [基本包装类型](#基本包装类型)
			* [引用类型](#引用类型)
	* [代码规范](#代码规范)
			* [加分号](#加分号)
			* [使用`''` 而不是`""`](#使用-而不是)
	* [作用域](#作用域)
			* [函数作用域](#函数作用域)
			* [不存在块级作用域](#不存在块级作用域)
			* [变量声明的提升](#变量声明的提升)
			* [闭包解决作用域问题](#闭包解决作用域问题)
	* [深浅拷贝](#深浅拷贝)
	* [隐式的强制转换](#隐式的强制转换)
			* [= 和 == 和 ===](#和-和)
			* [赋值`=`](#赋值)
			* [`==` 和 `===`](#和)
	* [if](#if)
	* [类方法 和 实例方法](#类方法-和-实例方法)

<!-- /code_chunk_output -->

# HTML

1. doctype
2. meta
3. SEO
4. 页面通讯 storage
5. HTML5标签 ie9不支持
6. viewport移动端缩放
7. 从浏览器上输入一个url后究竟发生了什么
8. `repaint` 和 `reflow`
9. 对于同个域名大多数浏览器加载资源(img，css，js等)的上限是6个
10. 事件捕获，事件冒泡，事件委托

# CSS

1. 0不加单位
2. 颜色值三位表示`#000`
3. BFC, IFC
4. 2种盒子模型(ie是width是包含border的)
5. box-sizing 修改盒子的类型 border-box content-box
6. 命名规范 不写驼峰 用`-`连接， BEM规范
7. px em rem % 
8. `visibility` 和 `dispaly: none`


# JavaScript

## V8， node的历史，npm的诞生
<hr style="height: 1px"></hr>

一匹布那么长
<br>
<br>
<br>
## DOM、 BOM
#### `window.onload` 和 `DOMContentLoaded`
现代浏览器页面加载的流程： 
```
DOM树构建 -> 下载资源js, css -> css代码解析为CSSOM -> DOM+CSSOM 渲染树构建 -> 布局 -> 绘制
```  
但它们并非严格按照这个顺序，往往第一步未完成 第二第三步便开始

## 基本类型 和 引用类型
<hr style="height: 1px"></hr>

#### 基本类型
- `undefined` `null` `string` `boolean` `number`  5种基本类型
- `symbol`    es6新增的基本类型
- `object`  复杂类型，==注意它不是基本类型==
- `undefined`由`null`派生而来
- `typeof null == 'object' // true, 因为null是空的对象引用` 
- `typeof`是操作符，它可能返回的值有`undefined` `boolean` `string` `number` `object` `function`
- `String` `Number` `Boolean`这3个其实是个构造函数，都是`Function`的实例
- ```javascript
  /*
   * String() 与 new String()的差别 
   */
  var str1 = new String('abc')    //  String对象的实例
  console.log(typeof str1)        //  "object"
  var str2 = String(123)          //  类型转换函数
  console.log(typeof str2)        //  "string"
  ```
-  **基本类型最突出的特征是它们的值是不可变的**
- ```javascript
  var person = 'shiro';
  console.log(person.toUpperCase()) //  "SHIRO"
  console.log(person)               //  "shiro"
  person.age = 22;
  person.method = function(){//...};
 
  console.log(person.age);          //  undefined
  console.log(person.method);       //  undefined
  ```
####  基本包装类型

####  引用类型
- 除了以上的6种基本类型，其余的都是引用类型
> `javascript`和其他语言不同，其不允许直接访问内存中的位置，也就是说不能直接操作对象的内存空间，那我们操作啥呢？ 实际上，是操作对象的引用，所以引用类型的值是按引用访问的。
准确地说，引用类型的存储需要内存的栈区和堆区（堆区是指内存里的堆内存）共同完成，栈区内存保存变量标识符和指向堆内存中该对象的指针，也可以说是该对象在堆内存的地址。

设有已下3个对象
```javascript
var person1 = {}
var person2 = {}
var person3 = {}
```

![img1](/assets/img1.png)


<br>
<br>

## 代码规范
<hr style="height: 1px"></hr>


#### 加分号
目前ESLint有两种流派`Airbnb`和`Standard` 前者推荐加分号，后者不推荐
个人推荐还是加
#### 使用`''` 而不是`""`
```javascript
function test() {
  return
  'hhhh';
}
console.log(test());

```
需要注意的是`return`它会自动在行尾加上分号的，所以它会输出什么？
<br>
<br>

## 作用域
<hr style="height: 1px"></hr>

#### 函数作用域

#### 不存在块级作用域
#### 变量声明的提升
```javascript
console.log(a);   // undefined
var a = 1;
```
`var a`声明会被提升到最顶，但赋值并不会。 所以`a`是`undefined`

函数声明也是会提升
```javascript
test();     //  输出'Hello world'
function test() {
  console.log('Hello world');
}

//  但是这种,则不会提升
test();     //  报错
var test = function() {
  console.log('Hello world');
}
```

#### 闭包解决作用域问题
<br>
<br>

## 深浅拷贝
<hr style="height: 1px"></hr>

这就是浅拷贝，`js`是引用的赋值
```javascript
var a = [1,2,3];
var b = a;
b[0] = 4;
console.log(a);   //  [4,2,3]
console.log(b);   //  [4,2,3]
```
数组使用`slice`和`concat`进行拷贝

对象的拷贝则只能自行实现
```javascript
Object.clone = function (source) {
  var o = {};
  for(var key in source) {
    o[key] = source[key];
  }
  return o;
}
```
## 隐式的强制转换
#### = 和 == 和 ===
<hr style="height: 1px"></hr>

#### 赋值`=`
对于基本类型`=`是==值==的传递
对于引用类型`=`则是==引用==的传递, 例如`var a = {}; var b = a` 其中`a`和`b`是指向同一个内存的

#### `==` 和 `===`

**基本类型之间的比较** 
  
  ```javascript
  null == undefined  // true
  0 == ''            // true
  0 == false         // true 
  NaN == NaN         // false
  'false' == false   // false
  'false' == true    // false

  0 == null          // false   特例, 虽然Number(null) = 0
  0 == undefined     // false
  ```
`==`它会把左右的数值转成`number`然后再进行对比， 即`Number(0) == Number(false)`
>  `Number()`对对象进行转换的时候，先会找对象是否实现了`valueOf()`方法，若无则执行`toString()`方法，再对这2个函数的返回值进行转换

>  ==注意==: 对于`'001'` `'123'`这些数字字符串(包括其前面的`+` `-`)， 一律忽略其前导的`0`，且将其转为十进制。 但对于`0xf`这种十六进制，则是转为与其等值的十进制

**基本类型 与 引用类型 之间的比较** 

  ```javascript
  0 == []            //  true   [].toString() = ''
  0 == {}            //  false
  null == {}         //  false
  null == []         //  false
  '' == []           //  true
  '' == {}           //  false
  ```
也是把左右两边转成`Number`进行比较

**引用类型之间的比较**
```javascript
[] == []    //  false
{} == {}    //  false
```
引用类型时按引用访问的，换句话说就是比较两个对象的堆内存中的地址是否相同。
 

  <br>
  <br>

## if
<hr style="height: 1px"></hr>

```javascript
if('false') {
    console.log('Hello world')
} //   输出'Hello world'
```
if语句会把 `'false'`转成 `bool`值
`Boolean('false') == true     //  true`
> tips: 使用`!!`来进行布尔值的强制转换

> `javascript`的七大假值`false` `0` `-0` `""` `NaN` `null` `undefined`

<br>
<br>

## 类方法 和 实例方法
<hr style="height: 1px"></hr>



**参考文章**
http://www.cnblogs.com/focusxxxxy/p/6390536.html 
http://www.jianshu.com/p/c1dfc6caa520 