---
title: React
date: 2023-01-01 00:00:00
tags: React
layout: aboutReact
---
# 1. React 入门概述

## 1.1 介绍

用于动态构建用户界面的 JavaScript 库(只关注于视图)

	1.发送请求获取数据
	2.处理数据（过滤，整理格式等）
	3.操作DOM呈现页面（React做的事情）
	
React是一个将数据渲染为HTML视图的开源JavaScript库

## 1.2 原生JavaScript的缺点

	1. 原生JavaScript操作DOM繁琐，效率低（DOM-API操作UI）
	2. 使用JavaScript直接操作DOM，浏览器会进行大量的重绘重排
	3. 原生JavaScript没有组件化编码方案，代码复用率很低
	
【补充】浏览器重绘重排

浏览器重绘(repaint)重排(reflow)与优化[浏览器机制]

**重绘**(repaint)：当一个元素的外观发生改变，但没有改变布局,重新把元素外观绘制出来的过程，叫做重绘

**重排**(reflow)：当DOM的变化影响了元素的几何信息(DOM对象的位置和尺寸大小)，浏览器需要重新计算元素的几何属性，将其安放在界面中的正确位置，这个过程叫做重排

##【补充】模块化与组件化

	• 模块
		1. 理解：向外提供特定功能的js程序, 一般就是一个js文件
		2. 为什么要拆成模块：随着业务逻辑增加，代码越来越多且复杂。
		3. 作用：复用js, 简化js的编写, 提高js运行效率
		
	• 组件
		1. 理解：用来实现局部功能效果的代码和资源的集合(html/css/js/image等等)
		2. 为什么要用组件： 一个界面的功能更复杂
		3. 作用：复用编码, 简化项目编码, 提高运行效率
		
模块化：当应用的js都以模块来编写的, 这个应用就是一个模块化的应用

组件化：当应用是以多组件的方式实现, 这个应用就是一个组件化的应用

## 1.3 React的特点

	1. 采用组件化模式、声明式编码，提高开发效率及组件复用率
	2. 在 React Native中可以使用React语法进行移动端开发
	3. 使用虚拟DOM+Diff算法，尽量减少与真实DOM的交互
	
## 1.4. React高效的原因

	1. 使用虚拟(virtual)DOM, 不总是直接操作页面真实DOM。

	2. DOM Diffing算法, 最小化页面重绘。
	
# 2. Hello React

## 2.1 相关库介绍

	• 旧版本 16.8.4 (March 5, 2019)
	• 新版本 有不一样的会说明
	
	1. react.js：React核心库。
	2. react-dom.js：提供操作DOM的React扩展库。
	3. babel.min.js：解析JSX语法代码转为JS代码的库。
	
## 【补充】babel.js的作用

	1. 浏览器不能直接解析JSX代码, 需要babel转译为纯JS的代码才能运行
	2. 只要用了JSX，都要加上type="text/babel", 声明需要babel来处理
	
## 2.2 使用JSX创建虚拟DOM
```react
const VDOM= <h1>Hello,React</h1>
```
## 2.3 渲染虚拟DOM(元素)

	1. 语法: 
```react
	ReactDOM.render(virtualDOM, containerDOM)
```

	2. 作用: 将虚拟DOM元素渲染到页面中的真实容器DOM中显示


	3. 参数说明 
	
		1. 参数一: 纯js或jsx创建的虚拟dom对象
		
		2. 参数二: 用来包含虚拟DOM元素的真实dom元素对象(一般是一个div)
```javaScript		
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="UTF-8">
  <title>hello_react</title>
</head>

<body>
  <!-- 准备好一个“容器” -->
  <div id="test"></div>

  <!-- 引入react核心库 -->
  <script type="text/javascript" src="../js/react.development.js"></script>
  <!-- 引入react-dom，用于支持react操作DOM -->
  <script type="text/javascript" src="../js/react-dom.development.js"></script>
  <!-- 引入babel，用于将jsx转为js -->
  <script type="text/javascript" src="../js/babel.min.js"></script>

  <script type="text/babel"> /* 此处一定要写babel */
    //1.创建虚拟DOM
    const VDOM = <h1>Hello,React</h1> /* 此处一定不要写引号，因为不是字符串 */
    //2.渲染虚拟DOM到页面
    ReactDOM.render(VDOM,document.getElementById('test'))
  </script>
</body>

</html>
```
## 2.4 页面显示
<img width="451" alt="image" src="https://user-images.githubusercontent.com/117837871/216939381-0451d71f-c024-46bf-8fb1-ff25e775c093.png">

# 3. 创建虚拟DOM的两种方式

## 3.1 纯JS方式(一般不用)
```javaScript
<div id="test"></div>

<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>

<script type="text/javascript" > 
  //1.创建虚拟DOM
  const VDOM = React.createElement('h1',{id:'title'},
  React.createElement('span',{},'Hello,React'))
  //2.渲染虚拟DOM到页面
  ReactDOM.render(VDOM,document.getElementById('test'))
```

## 3.2 JSX方式

	JSX方式就是js创建虚拟DOM的语法糖
```javascript
<div id="test"></div>

<script type="text/javascript" src="../js/react.development.js"></script>
<script type="text/javascript" src="../js/react-dom.development.js"></script>
<script type="text/javascript" src="../js/babel.min.js"></script>

<script type="text/babel" > /* 此处一定要写babel */
    //1.创建虚拟DOM
    const VDOM = (  /* 此处一定不要写引号，因为不是字符串 */
        <h1 id="title">
            <span>Hello,React</span>
        </h1>
    )
    //2.渲染虚拟DOM到页面
    ReactDOM.render(VDOM,document.getElementById('test'))

</script>![image](https://user-images.githubusercontent.com/117837871/216940180-3b28dbc4-3910-4119-845f-4f3b124ecc95.png)
```

# 4. 虚拟DOM与真实DOM

打印输出虚拟DOM和真实DOM进行比较
```javascript
const VDOM = (  /* 此处一定不要写引号，因为不是字符串 */
    <h1 id="title">
        <span>Hello,React</span>
    </h1>
)
// 渲染虚拟DOM到页面
ReactDOM.render(VDOM,document.getElementById('test'))
constTDOM= document.getElementById('demo')
console.log('虚拟DOM',VDOM);
console.log('真实DOM',TDOM);
debugger;
```
看看虚拟DOM身上有哪些属性 
<img width="433" alt="image" src="https://user-images.githubusercontent.com/117837871/216941884-1eb6f1e5-c9f2-429b-b6e0-38214ffd8a06.png">

看看真实DOM身上有哪些属性 
<img width="448" alt="image" src="https://user-images.githubusercontent.com/117837871/216941911-7af3b347-61b2-4a52-93a3-c98240f22c6d.png">

	1. 虚拟DOM本质是Object类型的对象（一般对象）
	
	2. 虚拟DOM比较 “轻”，真实DOM比较 “重”，因为虚拟DOM是React内部在用，无需真实DOM上那么多的属性
	
	3. 虚拟DOM最终会被React转化为真实DOM，呈现在页面上

# 5. JSX入门

## 5.1 概述

	1. 全称: JavaScript XML
	
	2. React定义的一种类似于XML的JS扩展语法: JS + XML本质是React.createElement(component, props, ...children)方法的语法糖
	
	3. 作用: 用来简化创建虚拟DOM 
	
		1. 写法：var ele = <h1>Hello JSX!</h1>
		
		2. 注意1：它不是字符串, 也不是HTML/XML标签
		
		3. 注意2：它最终产生的就是一个JS对象
		
	4. 标签名任意: HTML标签或其它标签
	
	5. 标签属性任意: HTML标签属性或其它
	
## 5.2 基本语法规则

	1. 定义虚拟DOM时，不要写引号。
	
	2. 标签中混入JS表达式时要用 { }。
	
	3. 样式的类名指定不要用 class，要用 className。（因为class是ES6中类的关键字，所以不让用）
	
	4. 内联样式，要用 style={{ key:value }} 的形式去写。
	
	5. 只有一个根标签
	
	6. 标签必须闭合
	
	7. 标签首字母 
	
		1. 若小写字母开头，则将该标签转为html中同名元素，若html中无该标签对应的同名元素，则报错。

		2. 若大写字母开头，React就去渲染对应的组件，若组件没有定义，则报错。
		
## 【补充】 区分js表达式与js语句

	1. 表达式：一个表达式会产生一个值，可以放在任何一个需要值的地方，下面这些都是表达式：
	
		1. a
		
		2. a+b
		
		3. demo(1) // 函数调用表达式
		
		4. arr.map()
		
		5. function test () {}
		
	2. 语句(代码)，下面这些都是语句(代码)：【控制语句，控制代码走向，而不是产生值】
	
		1. if(){ }
		
		2. for(){ }
		
		3. switch( ){case:xxxx}
		
## 5.3 总结

	1. 遇到 < 开头的代码, 以标签的语法解析: html同名标签转换为html同名元素, 其它标签需要特别解析
	
	2. 遇到以 { 开头的代码，以JS语法解析: 标签中的js表达式必须用{ }包含

# 【React】面向组件编程 - 基本理解和使用 - 组件三大核心属性state-props-refs - 事件处理 - 非受控组件 - 受控组件 - 高阶函数

## 1 . 基本理解和使用
### 1.1 函数式组件

```javascript
//创建函数式组件
function MyCompontent(){
    console.log(this);//这里的this是undefined，因为babel编译后开启了严格模式
    return <h2>我是用函数定义的组件（适用于简单组件的定义）</h2>
}
//渲染组件到页面
ReactDOM.render(<MyCompontent/>,docement.getElementById('test'))
```
![image](https://user-images.githubusercontent.com/117837871/217765611-333f4b51-104d-478c-a907-c875c5ba30e0.png)

    执行了ReactDOM.render(<MyComponent/>.......之后，发生了什么？

    React解析组件标签，找到了MyComponent组件。

    发现组件是使用函数定义的，随后调用该函数，将返回的虚拟DOM转为真实DOM，随后呈现在页面中。

【补充】严格模式中的this
```javascript
function sayThis() {
  console.log(this)
}
sayThis() // Window {...}
```

```javascript
function sayThis2() {
  'use strict'
  console.log(this)
}
sayThis2() // undefined
```

如果不开启严格模式，直接调用函数，函数中的this指向window

如果开启了严格模式，直接调用函数，函数中的this是undefined

### 1.2 类式组件
```javascript
//创建类式组件
class MyCompontent extends React.compontent {
    render(){
	    //render是放在哪里的？—— MyComponent的原型对象上，供实例使用。
	    //render中的this是谁？—— MyComponent的实例对象 <=> MyComponent组件实例对象。
        return <h2>我是用类定义的组件(适用于【复杂组件】的定义)</h2>
    }
}
ReactDOM.render(<MyCompontent/>,document.querySelector('.test'))
```
![image](https://user-images.githubusercontent.com/117837871/217765681-3219dbba-ba4e-430b-89ab-491304411957.png)
![image](https://user-images.githubusercontent.com/117837871/217765719-0818ccdb-4d40-40c7-84ba-1556b6028719.png)


    执行了ReactDOM.render(<MyComponent/>.......之后，发生了什么？

    React解析组件标签，找到了MyComponent组件。
    
    发现组件是使用类定义的，随后new出来该类的实例，并通过该实例调用到原型上的render方法。

    将render返回的虚拟DOM转为真实DOM，随后呈现在页面中。

【补充】关于ES6中类的注意事项

类中的构造器不是必须要写的，要对实例进行一些初始化的操作，如添加指定属性时才写。

如果A类继承了B类，且A类中写了构造器，那么A类构造器中的super是必须要调用的。

类中所定义的方法，都放在了类的原型对象上，供实例去使用。

### 1.3 注意

组件名必须首字母大写

虚拟DOM元素只能有一个根元素

虚拟DOM元素必须有结束标签


重点关注下渲染类组件标签的基本流程

* React内部会创建组件实例对象
* 调用render()得到虚拟DOM, 并解析为真实DOM
* 插入到指定的页面元素内部

## 2. 组件实例的三大核心属性1: state 状态

### 2.1 理解

state是组件对象最重要的属性, 值是对象(可以包含多个key-value的组合)

组件被称为"状态机", 通过更新组件的state来更新对应的页面显示(重新渲染组件)

### 2.2 应用

需求: 定义一个展示天气信息的组件

默认展示天气炎热 或 凉爽

点击文字切换天气

#### 2.2.1 手动切换版

类式组件，在构造器中 初始化状态，在render中通过this.state 读取状态
```javascript
class Weather extends React.Copmpontent{
    contructor(prop){
        super(prop);
        //初始化状态
        this.state = {
            isHot: true
        }
    }
    render(){
        //读取状态
        const {isHot} = this.state
        return <h2>今天天气很{isHot ? '炎热' : '凉爽'}</h2>
    }
}
ReactDOM.render('<Weather/>',docement.querySelector('.test'));
```
![image](https://user-images.githubusercontent.com/117837871/217765896-b98139ee-c913-4141-9b3f-52c687cd07c8.png)

【补充】原生JavaScript绑定事件监听的三种方式
```javascript
<button id="btn1">按钮1</button>

<button id="btn2">按钮2</button>

<button onclick="demo()">按钮3</button>

<script type="text/javascript" >
  const btn1 = document.getElementById('btn1')
  btn1.addEventListener('click',()=>{
    alert('按钮1被点击了')
  })

  const btn2 = document.getElementById('btn2')
  btn2.onclick = ()=>{
    alert('按钮2被点击了')
  }

  function demo(){
    alert('按钮3被点击了')
  }
</script>
```

【补充】类中方法的this指向问题

类中定义的方法，在内部默认开启了局部的严格模式

开启严格模式，函数如果直接调用，this不会指向window，而是undefined
```javascript
class Person {
  constructor(name,age){
    this.name = name
    this.age = age
  }
  study(){
    //study方法放在了哪里？——类的原型对象上，供实例使用
    //通过Person实例调用study时，study中的this就是Person实例
    console.log(this);
  }
}
const p1 = new Person('tom',18)
p1.study() //通过实例调用study方法  Person
const x = p1.study
x() // 直接调用 undefined
```
#### 2.2.2 点击切换版'

```javascript
// 1.创建组件
class Weather extends React.Component {
	
  // 构造器调用几次？ ———— 1次
  constructor(props){
    console.log('constructor');
    super(props)
    // 初始化状态
    this.state = {isHot:false,wind:'微风'}
    // 解决 changeWeather 中 this 指向问题
    this.changeWeather = this.changeWeather.bind(this)
  }

  // render调用几次？ ———— 1+n次 1是初始化的那次 n是状态更新的次数
  render(){
    console.log('render');
    //读取状态
    const {isHot,wind} = this.state
    return <h1 onClick={this.changeWeather}>今天天气很{isHot ? '炎热' : '凉爽'}，{wind}</h1>
  }

  // changeWeather调用几次？ ———— 点几次调几次
  changeWeather(){
    // changeWeather放在哪里？ ———— Weather的原型对象上，供实例使用
    // 由于changeWeather是作为onClick的回调，所以不是通过实例调用的，是直接调用
    // 类中的方法默认开启了局部的严格模式，所以changeWeather中的this为undefined

    console.log('changeWeather');
    // 获取原来的isHot值
    const isHot = this.state.isHot
    // 严重注意：状态必须通过setState进行更新,且更新是一种合并，不是替换。
    this.setState({isHot:!isHot})
    // console.log(this);

    // 严重注意：状态(state)不可直接更改，下面这行就是直接更改！！！
    // this.state.isHot = !isHot //这是错误的写法
  }
}
//2.渲染组件到页面
ReactDOM.render(<Weather/>,document.getElementById('test'))
```
![image](https://user-images.githubusercontent.com/117837871/217765963-ceed33e2-9a84-4e6e-b591-ee0873ff1c45.png)

#### 2.2.3 精简代码（实际开发中这样写）

可以不写构造器，类中直接写赋值语句来初始化状态

不用bind来绑定this（赋值语句的形式+箭头函数）

```javascript
// 1.创建组件
class Weather extends React.Component{
  // 初始化状态
  state = {isHot:false,wind:'微风'}

  render(){
    const {isHot,wind} = this.state
    return <h1 onClick={this.changeWeather}>今天天气很{isHot ? '炎热' : '凉爽'}，{wind}</h1>
  }

  // 自定义方法————要用赋值语句的形式 + 箭头函数
  // 没有放在原型上，而是放在实例上
  changeWeather = () => {
    const isHot = this.state.isHot
    this.setState({isHot:!isHot})
  }
}
// 2.渲染组件到页面
ReactDOM.render(<Weather/>,document.getElementById('test'))
```
【补充】类中直接写赋值语句

在类中直接写赋值语句，等于是给类的实例对象添加属性且赋值

## #2.3 注意

组件中render方法中的this为组件实例对象

组件自定义的方法中this为undefined，如何解决？

    a)	强制绑定this: 通过函数对象的bind()

    b)	箭头函数 + 赋值语句

状态数据state，不能直接修改或更新。状态必须通过  setState() 进行更新, 且更新是一种合并，不是替换。



## 3. 组件实例的三大核心属性2: props

### 3.1 理解

每个组件对象都会有props(properties的简写)属性

组件标签的所有属性都保存在props中

### 3.2 作用

通过标签属性从组件外向组件内传递变化的数据

注意: 组件内部不可修改props数据，是只读的

### 3.3 尝试一下
```javascript
// 创建组件 
class Person extends React.Component{
  render() {
    //const {name, sex, age} = this.props 
    return (
      <ul>
        {/* <li>姓名：{name}</li> 
        <li>性别：{sex}</li> 
        <li>年龄：{age}</li>  */}
        <li>姓名：{this.props.name}</li> 
        <li>性别：{this.props.sex}</li> 
        <li>年龄：{this.props.age}</li>
      </ul>
    )
  }
}
// 渲染组件到页面上
ReactDOM.render(<Person name="yk" age="18" sex="男"/>, document.getElementById('test'))
```
![image](https://user-images.githubusercontent.com/117837871/217766032-9d58d0cf-c11c-44d5-8a96-8d2d1681b4c0.png)

### 3.4 使用指南

#### 3.4.1 内部读取某个属性值

this.props.name

### 3.4.2 扩展属性: 将对象的所有属性通过props传递（批量传递标签属性）

```javascript
ReactDOM.render(<Person name="yk" age="18" sex="男"/>, document.getElementById('test'))

const person = {name: 'yk', age: 18, sex: '男'}

ReactDOM.render(<Person { ...person }/>, document.getElementById('test'))
```

【补充】展开运算符
```javascript

let arr1 = [1, 3, 5, 7, 9]

let arr2 = [2, 4, 6, 8, 10]

// 1. 展开一个数组

console.log(...arr1); // 1 3 5 7 9

// 2. 连接数组

let arr3 = [...arr1, ...arr2] // [1,3,5,7,9,2,4,6,8,10]

// 3. 在函数中使用
function sum(...numbers) {
    //求和！preValue前一个数，currentValue当前数
  return numbers.reduce((preValue, currentValue) => {
    return preValue + currentValue
  })
}
console.log(sum(1, 2, 3, 4)); // 10

// 4. 构造字面量对象时使用展开语法
let person = {
  name: 'tom',
  age: 18
}

// console.log(...person); // 报错，展开运算符不能展开对象
console.log({...person}) // {name: "tom", age: 18}
//babel+react使得可以使用展开运算符，但仅仅实用于标签属性的传递，如下⬇️
let person2 = { ...person } // 可以拷贝一个对象
person.name = 'jerry'
console.log(person2); // {name: "tom", age: 18}
console.log(person); // {name: "jerry", age: 18}

// 5. 合并对象
let person3 = {
  ...person,
  name: 'trumen',
  address: "上海"
}
console.log(person3); // {name: "trumen", age: 18, address: "上海"}
```

### 3.4.3 对props中的属性值进行类型限制和必要性限制

* 1. 第一种方式（React v15.5 开始已弃用）

直接写

```javascript
Person.propTypes = {
  name: React.PropTypes.string.isRequired,
  age: React.PropTypes.number
}
```

* 2. 第二种方式（新）：使用prop-types库进限制（需要引入prop-types库）

<!-- 引入prop-types，用于对组件标签属性进行限制 -->

<script type="text/javascript" src="../js/prop-types.js"></script>

```javascript
//对标签属性进行类型、必要性的限制
Person.propTypes = {
  name:PropTypes.string.isRequired, // 限制name必传，且为字符串
  sex:PropTypes.string, // 限制sex为字符串
  age:PropTypes.number, // 限制age为数值
  speak:PropTypes.func, // 限制speak为函数
}
```

可以写在类的里面，前面加static关键字

#### 3.4.4 默认属性值

```javascript
//指定默认标签属性值

Person.defaultProps = {
  sex:'男', // sex默认值为男
  age:18 //age默认值为18
}
```

可以写在类的里面，前面加static关键字

#### 3.4.5 组件类的构造函数

```javascript
constructor(props){
  super(props)
  console.log(this.props)//打印所有属性
}
```

* 构造器是否接收props，是否传递给super，取决于：是否希望在构造器中通过this访问props

### 3.5 应用

需求: 自定义用来显示一个人员信息的组件

姓名必须指定，且为字符串类型；

性别为字符串类型，如果性别没有指定，默认为男

年龄为数字类型，默认值为18

```javascript
//创建组件
class Person extends React.Component{

  //对标签属性进行类型、必要性的限制
  static propTypes = {
    name:PropTypes.string.isRequired, //限制name必传，且为字符串
    sex:PropTypes.string,//限制sex为字符串
    age:PropTypes.number,//限制age为数值
  }

  //指定默认标签属性值
  static defaultProps = {
    sex:'男',//sex默认值为男
    age:18 //age默认值为18
  }

  render(){
    // console.log(this);
    const {name,age,sex} = this.props
    //props是只读的
    //this.props.name = 'jack' //此行代码会报错，因为props是只读的
    return (
      <ul>
        <li>姓名：{name}</li>
        <li>性别：{sex}</li>
        <li>年龄：{age+1}</li>
      </ul>
    )
  }
}

//渲染组件到页面
ReactDOM.render(<Person name="jerry"/>,document.getElementById('test1'))
```

### 3.6 函数式组件使用props

```javascript
//创建组件
function Person (props){
  const {name,age,sex} = props
    return (
      <ul>
        <li>姓名：{name}</li>
        <li>性别：{sex}</li>
        <li>年龄：{age}</li>
      </ul>
    )
}

//对标签属性进行类型、必要性的限制
Person.propTypes = {
  name:PropTypes.string.isRequired, //限制name必传，且为字符串
  sex:PropTypes.string,  //限制sex为字符串
  age:PropTypes.number,  //限制age为数值
}

// 指定默认标签属性值
Person.defaultProps = {
  sex:'男',// sex默认值为男
  age:18 // age默认值为18
}

//渲染组件到页面
ReactDOM.render(<Person name="jerry"/>,document.getElementById('test1'))
```

## 4. 组件三大核心属性3: refs与事件处理

### 4.1 理解

组件内的标签可以定义ref属性来标识自己

### 4.2 应用

需求: 自定义组件, 功能说明如下

点击按钮, 提示第一个输入框中的值

当第2个输入框失去焦点时, 提示这个输入框中的值


## 4.3 编码

### 4.3.1 字符串形式的ref（** 新版本不推荐使用了 **）

1. 定义
<input ref="input1"/>

2. 使用
this.refs.input1

3. 示例
```javascript
//创建组件
class Demo extends React.Component{
  //展示左侧输入框的数据
  showData = ()=>{
    const {input1} = this.refs
    alert(input1.value)
  }
  //展示右侧输入框的数据
  showData2 = ()=>{
    const {input2} = this.refs
    alert(input2.value)
  }
  
  render(){
    return(
      <div>
        <input ref="input1" type="text" placeholder="点击按钮提示数据"/>&nbsp;
        <button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
        <input ref="input2" onBlur={this.showData2} type="text" placeholder="失去焦点提示数据"/>
      </div>
    )
  }
}
//渲染组件到页面
ReactDOM.render(<Demo />,document.getElementById('test'))
```

### 4.3.2 回调形式的ref

1. 定义

```javascript
<input ref={(currentNode)=>{this.input1 = currentNode}} />
```

简写一下

```javascript
<input ref={ c => this.input1 = c } />
```

2. 使用

this.input1

3. 示例

```javascript
//创建组件
class Demo extends React.Component{
  //展示左侧输入框的数据
  showData = ()=>{
    //从实例自身取
    const {input1} = this
    alert(input1.value)
  }
  //展示右侧输入框的数据
  showData2 = ()=>{
    const {input2} = this
    alert(input2.value)
  }
  
  render(){
    return(
      <div>
        <input ref={ c => this.input1 = c } type="text" placeholder="点击按钮提示数据"/>&nbsp;
        <button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
        <input onBlur={this.showData2} ref={c => this.input2 = c } type="text" placeholder="失去焦点提示数据"/>&nbsp;
      </div>
    )
  }
}
//渲染组件到页面
ReactDOM.render(<Demo />,document.getElementById('test'))
```

4. 回调执行次数

![image](https://user-images.githubusercontent.com/117837871/218298374-9f3931c3-ea0d-45a5-80c2-cd4b15e1a51f.png)

![image](https://user-images.githubusercontent.com/117837871/218298384-a6b30e7b-a208-408e-b0ca-27d979d71fe6.png)

内联的回调，渲染时调用一次，每次更新都会执行两次

类绑定的回调，就在初始渲染时调用一次

影响不大，日常开发基本都用内联，方便一点

### 4.3.3 createRef创建ref容器

1. 定义

```javascript
// React.createRef调用后可以返回一个容器
// 该容器可以存储被ref所标识的节点,该容器是“专人专用”的
myRef = React.createRef() 

<input ref={this.myRef}/>
```
2. 使用

this.myRef.current

3. 示例

```javascript
//创建组件
class Demo extends React.Component{

  myRef = React.createRef()
  myRef2 = React.createRef()
  //展示左侧输入框的数据
  showData = ()=>{
    alert(this.myRef.current.value);
  }
  //展示右侧输入框的数据
  showData2 = ()=>{
    alert(this.myRef2.current.value);
  }
  
  render(){
    return(
      <div>
        <input ref={this.myRef} type="text" placeholder="点击按钮提示数据"/>&nbsp;
        <button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
        <input onBlur={this.showData2} ref={this.myRef2} type="text" placeholder="失去焦点提示数据"/>&nbsp;
      </div>
    )
  }
}
//渲染组件到页面
ReactDOM.render(<Demo />,document.getElementById('test'))
```

## 5. React中的事件处理

通过onXxx属性指定事件处理函数(注意大小写)

React使用的是自定义(合成)事件, 而不是使用的原生DOM事件----为了更好的兼容性

React中的事件是通过事件委托方式处理的(委托给组件最外层的元素) ----为了的高效

通过event.target得到发生事件的DOM元素对象----不要过度使用ref

发生事件的元素是需要操作的元素时，可以避免使用ref

```javascript
//创建组件
class Demo extends React.Component{

  //创建ref容器
  myRef = React.createRef()
  // myRef2 = React.createRef()

  //展示左侧输入框的数据
  showData = (event)=>{
    console.log(event.target); // <button>点我提示左侧的数据</button>
    alert(this.myRef.current.value);
  }

  //展示右侧输入框的数据
  showData2 = (event)=>{
    alert(event.target.value);
  }

  render(){
    return(
      <div>
        <input ref={this.myRef} type="text" placeholder="点击按钮提示数据"/>&nbsp;
        <button onClick={this.showData}>点我提示左侧的数据</button>&nbsp;
        <input onBlur={this.showData2} type="text" placeholder="失去焦点提示数据"/>&nbsp;
      </div>
    )
  }
}
//渲染组件到页面
ReactDOM.render(<Demo />,document.getElementById('test'))
```


## 6. 收集表单数据

### 6.1 理解

包含表单的组件分类

受控组件

非受控组件

### 6.2 应用

需求:

定义一个包含表单的组件

输入用户名密码后, 点击登录提示输入信息

### 6.3 非受控组件

页面中所有输入类DOM的值，都是现用现取的

```javascript
// 创建组件
class Login extends React.Component {
  handleSubmit = (event) => {
    event.preventDefault() // 阻止表单提交
    const {username, password} = this
    alert(`您输入的用户名是 ${username.value}，您输入的密码是：${password.value}`)
  }
  render() {
    return (
      <form action="https://www.baidu.com/" onSubmit={this.handleSubmit}>
        用户名：<input ref={c => this.username = c} type="text" name="username" />
        密码：<input ref={c => this.password = c} type="password" name="password" />
        <button>登录</button>  
      </form>
    )
  }
}
// 渲染组件
ReactDOM.render(<Login />, document.getElementById('test'))
```

## 6.4 受控组件

页面中输入类的DOM，随着输入的过程，将数据存储在状态state中，需要用的时候在从状态state中取（有点类似Vue中的双向数据绑定）

```javascript
// 创建组件
class Login extends React.Component {
  // 初始化状态
  state = {
    username: '',
    password: ''
  }
  // 保存用户名到状态中
  saveUsername = (event) => {
    this.setState({username: event.target.value})
  }
  // 保存密码到状态中
  savePassword = (event) => {
    this.setState({password: event.target.value})
  }
  // 表单提交的回调
  handleSubmit = (event) => {
    event.preventDefault()
    const {username, password} = this.state
    alert(`您输入的用户名是 ${username}，您输入的密码是：${password}`)
  }

  render() {
    return (
      <form action="https://www.baidu.com/" onSubmit={this.handleSubmit}>
        用户名：<input onChange={this.saveUsername} type="text" name="username" />
        密码：<input onChange={this.savePassword} type="password" name="password" />
        <button>登录</button>  
      </form>
    )
  }
}
// 渲染组件
ReactDOM.render(<Login />, document.getElementById('test'))
```

## 7. 高阶函数与函数的柯里化

### 7.1 高阶函数

高阶函数：如果一个函数符合下面2个规范中的任何一个，那该函数就是高阶函数。

若A函数，接收的参数是一个函数，那么A就可以称之为高阶函数。

若A函数，调用的返回值依然是一个函数，那么A就可以称之为高阶函数。

常见的高阶函数有：Promise、setTimeout、arr.map()等等

### 7.2 函数的柯里化

函数的柯里化：通过函数调用继续返回函数的方式，实现多次接收参数最后统一处理的函数编码形式。

```javascript
function sum1(a, b, c){
  return a + b + c;
}
sum1(1, 2, 3)

// 柯里化后
function sum(a){
  return(b)=>{
    return (c)=>{
      return a+b+c
    }
  }
}
sum(1)(2)(3)
```

### 7.3 利用高阶函数与函数柯里化简写6.4的代码

必须传一个函数作为onChange事件的回调

```javascript
//创建组件
class Login extends React.Component{
  //初始化状态
  state = {
    username:'', //用户名
    password:'' //密码
  }

  //保存表单数据到状态中 （高阶函数+函数柯里化）
  saveFormData = (dataType)=>{
    return (event)=>{
      this.setState({[dataType]:event.target.value})
    }
  }

  //表单提交的回调
  handleSubmit = (event)=>{
    event.preventDefault() //阻止表单提交
    const {username,password} = this.state
    alert(`你输入的用户名是：${username},你输入的密码是：${password}`)
  }
  render(){
    return(
      <form onSubmit={this.handleSubmit}>
        用户名：<input onChange={this.saveFormData('username')} type="text" name="username"/>
        密码：<input onChange={this.saveFormData('password')} type="password" name="password"/>
        <button>登录</button>
      </form>
    )
  }
}
//渲染组件
ReactDOM.render(<Login/>,document.getElementById('test'))
```

### 7.4 不用柯里化实现7.3

```javascript
//保存表单数据到状态中
saveFormData = (dataType,event)=>{
  this.setState({[dataType]:event.target.value})
}

render(){
  return(
	<form onSubmit={this.handleSubmit}>
	  用户名：<input onChange={ event => this.saveFormData('username',event) } type="text" name="username"/>
	  密码：<input onChange={ event => this.saveFormData('password',event) } type="password" name="password"/>
	  <button>登录</button>
	</form>
  )
}
```
# 组件的生命周期 - 虚拟DOM - DOM Diffing算法

## 1. 组件的生命周期

### 1.1 理解

组件从创建到死亡它会经历一些特定的阶段。

React组件中包含一系列勾子函数(生命周期回调函数), 会在特定的时刻调用。

我们在定义组件时，会在特定的生命周期回调函数中，做特定的工作。

### 1.2 引入案例

需求:定义组件实现以下功能：

让指定的文本做显示 / 隐藏的渐变动画

从完全可见，到彻底消失，耗时2S

点击“不活了”按钮从界面中卸载组件

```javascript
//创建组件
//生命周期回调函数 <=> 生命周期钩子函数 <=> 生命周期函数 <=> 生命周期钩子
class Life extends React.Component{

  state = {opacity:1}

  death = ()=>{
    // 清除定时器
    // clearInterval(this.timer)
    // 卸载组件
    ReactDOM.unmountComponentAtNode(document.getElementById('test'))
  }

  // 组件挂载完毕
  componentDidMount(){
    console.log('componentDidMount');
    this.timer = setInterval(() => {
      //获取原状态
      let {opacity} = this.state
      //减小0.1
      opacity -= 0.1
      if(opacity <= 0) opacity = 1
      //设置新的透明度
      this.setState({opacity})
    }, 200);
  }

  // 组件将要卸载
  componentWillUnmount(){
    // 清除定时器
    clearInterval(this.timer)
  }

  // 初始化渲染、状态更新之后 调用1+n次
  render(){
    console.log('render');
    return(
      <div>
        <h2 style={{opacity:this.state.opacity}}>React学不会怎么办？</h2>
        <button onClick={this.death}>不活了</button>
      </div>
    )
  }
}
//渲染组件
ReactDOM.render(<Life/>,document.getElementById('test'))
```

![image](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fc4090cc0a5f44248e534fec82ab82d2~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image)

https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/fc4090cc0a5f44248e534fec82ab82d2~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image

### 1.3 生命周期的三个阶段（旧）

![image](https://user-images.githubusercontent.com/117837871/218704757-f4bd7825-9d5d-4eb6-89fe-2c33532ac4aa.png)

v16.8.4

#### 1.3.1 初始化阶段

由**ReactDOM.render()**触发---初次渲染

1.**constructor()**—— 类组件中的构造函数

2.**componentWillMount()** —— 组件将要挂载 【即将废弃】

3.**render()**  —— 挂载组件

4.**componentDidMount()** —— 组件挂载完成 比较常用：

一般在这个钩子中做一些初始化的事，例如：开启定时器、发送网络请求、订阅消息

```javascript
class Count extends React.Component{

  // 构造器
  constructor(props){
    alert('constructor')
	console.log('Count---constructor');
	super(props)
	// 初始化状态
	this.state = {count:0}
  }
  // state = {count:0}
  add = () => {
    const {count} = this.state
    this.setState({count: count+1})
  }
  
  //组件将要挂载的钩子【即将废弃】
  componentWillMount(){
    alert('componentWillMount')
    console.log('Count---componentWillMount');
  }

  // 挂载组件
  render(){
    alert('render')
    console.log('Count---render');
    const {count} = this.state
    return(
      <div>
        <h1>当前计数值：{count}</h1>
        <button onClick={this.add}>点我+1</button>
      </div>
    )
  }

  //组件挂载完毕的钩子
  componentDidMount(){
    alert('componentDidMount')
	console.log('Count---componentDidMount');
  }
}
ReactDOM.render(<Count/>, document.getElementById('test'))
```

![image](https://user-images.githubusercontent.com/117837871/218704847-ae672973-44d9-44c1-b65c-45a8751596e1.png)
https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/7505801778224e368ee9f40edf2d2642~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.image

#### 1.3.2 更新阶段

【第一种情况】父组件重新**render**触发

**componentWillReceiveProps()** —— 接收属性参数（非首次）【即将废弃】

然后调用下面的钩子函数*

【第二种情况】由组件内部**this.setSate()**

**shouldComponentUpdate()** —— 组件是否应该被更新（默认返回true）

然后调用下面的钩子函数

【第三种情况】强制更新 **forceUpdate()**

**componentWillUpdate()** ——组件将要更新 【即将废弃】

**render()** —— 组件更新

**componentDidUpdate()** —— 组件完成更新


#### 1.3.3 卸载组件

由**ReactDOM.unmountComponentAtNode()**触发

**componentWillUnmount()** —— 组件即将卸载


### 1.4 生命周期的三个阶段（新）

![image](https://user-images.githubusercontent.com/11783  7871/218704912-83a52735-9acc-42e0-9cc6-83e6d752122f.png)

v17.0.1

##### 1. 初始化阶段

由**ReactDOM.render()**触发 —— 初次渲染

* **constructor()** —— 类组件中的构造函数

* **static getDerivedStateFromProps(props, state)** 从props得到一个派生的状态【新增】

* **render()** —— 挂载组件

* **componentDidMount()** —— 组件挂载完成 比较==常用==

##### 2. 更新阶段

由组件内部**this.setSate()**或父组件**重新render**触发或强制更新**forceUpdate()**

* **getDerivedStateFromProps()** —— 从props得到一个派生的状态  【新增】

* **shouldComponentUpdate()** —— 组件是否应该被更新（默认返回true）

* **render()** —— 挂载组件

* **getSnapshotBeforeUpdate()** —— 在更新之前获取快照【新增】

* **componentDidUpdate(prevProps, prevState, snapshotValue)** —— 组件完成更新

##### 3. 卸载组件

* 由ReactDOM.unmountComponentAtNode()触发

* **componentWillUnmount()** —— 组件即将卸载

### 1.5 重要的勾子

**render**：初始化渲染或更新渲染调用

**componentDidMount**：开启监听, 发送ajax请求

**componentWillUnmount**：做一些收尾工作, 如: 清理定时器

### 1.6 即将废弃的勾子

componentWillMount

componentWillReceiveProps

componentWillUpdate

现在使用会出现警告，下一个大版本需要加上UNSAFE_前缀才能使用，以后可能会被彻底废弃，不建议使用。

## 2. 虚拟DOM与DOM Diffing算法

### 2.1 基本原理图

![image](https://user-images.githubusercontent.com/117837871/218704968-244b5f61-9cad-4458-8fcf-fa62ba1e00ab.png)

详细的原理可以看之前在学Vue源码时的关于diff的笔记【Vue源码】图解 diff算法 与 虚拟DOM-snabbdom-最小量更新原理解析-手写源码-

### 2.2 关于key的经典面试题

react/vue中的key有什么作用？（key的内部原理是什么？）

为什么遍历列表时，key最好不要用index?

#### 2.2.1 虚拟DOM中key的作用

简单的说: key是虚拟DOM对象的标识, 在更新显示时key起着极其重要的作用。

详细的说: 当状态中的数据发生变化时，react会根据【新数据】生成【新的虚拟DOM】, 随后React进行【新虚拟DOM】与【旧虚拟DOM】的diff比较，比较规则如下：

旧虚拟DOM中找到了与新虚拟DOM相同的key：

若虚拟DOM中内容没变, 直接使用之前的真实DOM

若虚拟DOM中内容变了, 则生成新的真实DOM，随后替换掉页面中之前的真实DOM


旧虚拟DOM中未找到与新虚拟DOM相同的key

根据数据创建新的真实DOM，随后渲染到到页面


#### 2.2.2 用index作为key可能会引发的问题

若对数据进行：逆序添加、逆序删除等破坏顺序操作: 会产生没有必要的真实DOM更新 ==> 界面效果没问题, 但效率低


如果结构中还包含输入类的DOM：会产生错误DOM更新 ==> 界面有问题


注意！如果不存在对数据的逆序添加、逆序删除等破坏顺序操作，仅用于渲染列表用于展示，使用index作为key是没有问题的


2.2.3 开发中如何选择key?

最好使用每条数据的唯一标识作为key, 比如id、手机号、身份证号、学号等唯一值

如果确定只是简单的展示数据，用index也是可以的
# 使用create-react-app创建react应用


## 1.1. react脚手架

1.xxx脚手架: 用来帮助程序员快速创建一个基于xxx库的模板项目

* 包含了所有需要的配置（语法检查、jsx编译、devServer…）

* 下载好了所有相关的依赖

* 可以直接运行一个简单效果

2.react提供了一个用于创建react项目的脚手架库: create-react-app

3.项目的整体技术架构为:  react + webpack + es6 + eslint

4.使用脚手架开发的项目的特点: 模块化, 组件化, 工程化

## 1.2. 创建项目并启动

全局安装：**npm install -g create-react-app**

切换到想创项目的目录，使用命令：**create-react-app hello-react**

进入项目文件夹：**cd hello-react**

启动项目：**npm start**

![image](https://user-images.githubusercontent.com/117837871/220043507-be6a541b-0555-45ef-9f6b-3b4d3d7f2933.png)

![image](https://user-images.githubusercontent.com/117837871/220043555-34074e8d-6f6e-4465-b3f4-3b66839e455d.png)


## 1.3. react脚手架项目结构

public ---- 静态资源文件夹

	favicon.icon ------ 网站页签图标

	index.html -------- 主页面

	logo192.png ------- logo图

	logo512.png ------- logo图

	manifest.json ----- 应用加壳的配置文件

	robots.txt -------- 爬虫协议文件

src ---- 源码文件夹

	App.css -------- App组件的样式

	App.js --------- App组件

	App.test.js ---- 用于给App做测试
	
  index.css ------ 样式
	
  index.js ------- 入口文件
	
  logo.svg ------- logo图
	
  reportWebVitals.js --- 页面性能分析文件(需要web-vitals库的支持)
	
  setupTests.js ---- 组件单元测试的文件(需要jest-dom库的支持)


**>>index.html**
```javascript
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8" />
  <!-- %PUBLIC_URL%代表public文件夹的路径 -->
  <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
  <!-- 开启理想视口，用于做移动端网页的适配 -->
  <meta name="viewport" content="width=device-width, initial-scale=1" />
  <!-- 用于配置浏览器页签+地址栏的颜色(仅支持安卓手机浏览器) -->
  <meta name="theme-color" content="red" />
  <meta name="description" content="Web site created using create-react-app" />
  <!-- 用于指定网页添加到手机主屏幕后的图标 -->
  <link rel="apple-touch-icon" href="%PUBLIC_URL%/logo192.png" />
  
  <!--
    manifest.json provides metadata used when your web app is installed on a
    user's mobile device or desktop. See https://developers.google.com/web/fundamentals/web-app-manifest/
  -->
  <!-- 应用加壳时的配置文件 -->
  <link rel="manifest" href="%PUBLIC_URL%/manifest.json" />
  <!--
    Notice the use of %PUBLIC_URL% in the tags above.
    It will be replaced with the URL of the `public` folder during the build.
    Only files inside the `public` folder can be referenced from the HTML.

    Unlike "/favicon.ico" or "favicon.ico", "%PUBLIC_URL%/favicon.ico" will
    work correctly both with client-side routing and a non-root public URL.
    Learn how to configure a non-root public URL by running `npm run build`.
  -->
  <title>React App</title>
</head>

<body>
  <!-- 若浏览器不支持js则展示标签中的内容 -->
  <noscript>You need to enable JavaScript to run this app.</noscript>
  <div id="root"></div>
  <!--
    This HTML file is a template.
    If you open it directly in the browser, you will see an empty page.

    You can add webfonts, meta tags, or analytics to this file.
    The build step will place the bundled scripts into the <body> tag.

    To begin the development, run `npm start` or `yarn start`.
    To create a production bundle, use `npm run build` or `yarn build`.
  -->
</body>

</html>
```

**>>index.js**
```javascript
import React from 'react';
import ReactDOM from 'react-dom';
import './index.css';
import App from './App';
import reportWebVitals from './reportWebVitals';

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById('root')
);

// If you want to start measuring performance in your app, pass a function
// to log results (for example: reportWebVitals(console.log))
// or send to an analytics endpoint. Learn more: https://bit.ly/CRA-vitals
reportWebVitals();
```

**>>App.js**
```javascript
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header">
        <img src={logo} className="App-logo" alt="logo" />
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```

## 1.4. 功能界面的组件化编码流程（通用）

1.拆分组件: 拆分界面,抽取组件

2.实现静态组件: 使用组件实现静态页面效果

3.实现动态组件

* 动态显示初始化数据

  * 数据类型

  * 数据名称

  * 保存在哪个组件

* 交互(从绑定事件监听开始)


# 2. 脚手架版 Hello React

## 2.1 注意事项

  1.为了区分组件和普通js文件，可以把定义组件的js文件后缀改成jsx

  2.一个组件一个文件夹

  3.引入js文件或者jsx文件时，可以不写后缀名

  4.组件文件夹中的文件可以都命名为index，例如 index.jsx/index.css，引入的时候可以直接引到目录名就行了

## 2.2 文件目录

![image](https://user-images.githubusercontent.com/117837871/220043678-0443345f-4ad2-4437-a593-ef3bd9cba086.png)


## 2.3 代码

**>>index.html**
```javascript
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
    <title>React App</title>
  </head>
  <body>
    <div id="root"></div>
  </body>
</html>
```

**>>index.js**
```javascript
import React from "react";
import ReactDOM from "react-dom";
import App from "./App";

ReactDOM.render(
  <React.StrictMode>
    <App />
  </React.StrictMode>,
  document.getElementById("root")
);
```

**>>App.js**
```javascript
import React, { Component } from "react";
import Hello from "./components/Hello/Hello";
import Welcome from "./components/Welcome/Welcome";
export default class App extends Component {
  render() {
    return (
      <div>
        <Hello></Hello>
        <Welcome></Welcome>
      </div>
    );
  }
}
```

**>>Hello.jsx**
```javascript
import React, { Component } from "react";
import "./Hello.css";
export default class Hello extends Component {
  render() {
    return (
      <div>
        <h1 className="title">Hello React</h1>
      </div>
    );
  }
}
```

**>>Hello.css**
```javascript
.title {
  background-color: pink;
}
```

**>>Welcome.jsx**
```javascript
import React, { Component } from "react";
import "./Welcome.css";

export default class Welcome extends Component {
  render() {
    return <h2 className="demo">Welcome</h2>;
  }
}
```

**>>Welcome.css**
```javascript
.demo {
  background-color: skyblue;
}
```
## 2.4 页面

![image](https://user-images.githubusercontent.com/117837871/220043748-e4348946-70a0-4c1b-b839-a110a2ef6382.png)


# 3. VSCode生成代码模板

![image](https://user-images.githubusercontent.com/117837871/220043789-c8f7da4b-7405-4279-b1fd-f644c920d5dc.png)


rcc+回车 （react class component）

![image](https://user-images.githubusercontent.com/117837871/220043844-498fe04c-4675-4891-81b3-fcee7c9c1a97.png)


rfc（react function component）

```javascript
import React, { Component } from 'react'

export default class Demo extends Component {
  render() {
    return (
      <div>
        
      </div>
    )
  }
}
```
![image](https://user-images.githubusercontent.com/117837871/220043913-c6f6f826-a2e6-46d8-b6d6-befc49fc5948.png)

# 4. 样式的模块化
文件名保存为 **index.module.css**

引入文件 **import hello from './index.module.css'**

使用样式 **<h2 className={hello.title}> Hello </h2>**
# TodoList

## 1. 目标功能界面

![image](https://user-images.githubusercontent.com/117837871/220586710-8cda4354-1d15-44b3-8d2e-1196c43a9679.png)


## 2. 界面模块拆分

![image](https://user-images.githubusercontent.com/117837871/220586632-ce9102cb-724b-472c-b580-74e5c67dd91b.png)

![image](https://user-images.githubusercontent.com/117837871/220586897-9993ceae-c17b-4db0-b1fb-f51317040f25.png)



## 3. 主页 

**>>index.html**
```html
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8" />
  <link rel="icon" href="%PUBLIC_URL%/favicon.ico" />
  <title>React App</title>
</head>

<body>
  <div id="root"></div>
</body>

</html>
```

## 4. 静态页面搭建

**>>index.js**
```javascript
import React from "react";
import ReactDDOM from "react-dom";
import App from "./App";

ReactDOM.render(<App />, document.getElementById("root"));
```


**>>App.jsx**
```javascript
import React, { Component } from "react";
import Header from "./components/Header";
import List from "./components/List";
import Footer from "./components/Footer";
import './App.css'

export default class App extends Component {
  render() {
    return (
      <div className="todo-container">
        <div className="todo-warp">
          <Header />
          <List />
          <Footer />
        </div>
      </div>
    );
  }
}
```

**>>App.css**
```css
/*base*/
body {
  background: #fff;
}

.btn {
  display: inline-block;
  padding: 4px 12px;
  margin-bottom: 0;
  font-size: 14px;
  line-height: 20px;
  text-align: center;
  vertical-align: middle;
  cursor: pointer;
  box-shadow: inset 0 1px 0 rgba(255, 255, 255, 0.2), 0 1px 2px rgba(0, 0, 0, 0.05);
  border-radius: 4px;
}

.btn-danger {
  color: #fff;
  background-color: #da4f49;
  border: 1px solid #bd362f;
}

.btn-danger:hover {
  color: #fff;
  background-color: #bd362f;
}

.btn:focus {
  outline: none;
}

/*app*/
.todo-container {
  width: 600px;
  margin: 0 auto;
}
.todo-container .todo-wrap {
  padding: 10px;
  border: 1px solid #ddd;
  border-radius: 5px;
}
```

**>>Header/index.js**
```javascript
import React, { Component } from 'react'
import './index.css'

export default class Header extends Component {
  render() {
    return (
      <div className="todo-header">
        <input type="text" placeholder="请输入你的任务名称，按回车键确认"/>
      </div>
    )
  }
}
```


**>>Header/index.css**
```css
/*header*/
.todo-header input {
  width: 560px;
  height: 28px;
  font-size: 14px;
  border: 1px solid #ccc;
  border-radius: 4px;
  padding: 4px 7px;
}

.todo-header input:focus {
  outline: none;
  border-color: rgba(82, 168, 236, 0.8);
  box-shadow: inset 0 1px 1px rgba(0, 0, 0, 0.075), 0 0 8px rgba(82, 168, 236, 0.6);
}
```


**>>List/index.jsx**
```javascript
import React, { Component } from 'react'
import Item from '../Item'
import './index.css'

export default class List extends Component {
  render() {
    return (
      <ul className="todo-main">
        <Item />
      </ul>
    )
  }
}
```


**>>List/index.css**
```css
/*main*/
.todo-main {
  margin-left: 0px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding: 0px;
}

.todo-empty {
  height: 40px;
  line-height: 40px;
  border: 1px solid #ddd;
  border-radius: 2px;
  padding-left: 5px;
  margin-top: 10px;
}
```


**>>Item/index.jsx**
```javascript
import React, { Component } from 'react'
import './index.css'

export default class Item extends Component {
  render() {
    return (
      <li>
        <label>
          <input type="checkbox"/>
          <span>xxxxx</span>
        </label>
        <button className="btn btn-danger" style={{display:'none'}}>删除</button>
      </li>
    )
  }
}
```


**>>Item/index.css**
```css
/*item*/
li {
  list-style: none;
  height: 36px;
  line-height: 36px;
  padding: 0 5px;
  border-bottom: 1px solid #ddd;
}

li label {
  float: left;
  cursor: pointer;
}

li label li input {
  vertical-align: middle;
  margin-right: 6px;
  position: relative;
  top: -1px;
}

li button {
  float: right;
  display: none;
  margin-top: 3px;
}

li:before {
  content: initial;
}

li:last-child {
  border-bottom: none;
}
```


**>>Footer/index.jsx**
```javascript
import React, { Component } from 'react'
import './index.css'

export default class Footer extends Component {
  render() {
    return (
      <div className="todo-footer">
      <label>
        <input type="checkbox"/>
      </label>
      <span>
        <span>已完成0</span> / 全部2
      </span>
      <button className="btn btn-danger">清除已完成任务</button>
    </div>
    )
  }
}
```


**>>Footer/index.css**
```css
/*footer*/
.todo-footer {
  height: 40px;
  line-height: 40px;
  padding-left: 6px;
  margin-top: 5px;
}

.todo-footer label {
  display: inline-block;
  margin-right: 20px;
  cursor: pointer;
}

.todo-footer label input {
  position: relative;
  top: -1px;
  vertical-align: middle;
  margin-right: 5px;
}

.todo-footer button {
  float: right;
  margin-top: 5px;
}
```


## 5. 动态组件

### 5.1 动态初始化页面

状态驱动组件

考虑两个问题  要将状态放在哪？ 状态的存储形式是什么？


可以将状态放在需要使用状态的 父组件 App中，这样Header和List都可以通过props拿到状态数据


状态的存储形式采用对象数组


```javascript
// 初始化状态
state = {
  todos: [
    { id: '001', name: '吃饭', done: true },
    { id: '002', name: '睡觉', done: true },
    { id: '003', name: '敲代码', done: false },
  ]
}
```

**>>App.jsx**
```javascript
//在App.jsx组件中定义状态state，通过标签属性传递给子组件List的props中
export default class App extends Component {
  // 初始化状态
  state = {
    todos: [
      { id: '001', name: '吃饭', done: true },
      { id: '002', name: '睡觉', done: true },
      { id: '003', name: '敲代码', done: false },
    ]
  }
  render() {
    const  {todos} = this.state
    return (
      <div className="todo-container">
        <div className="todo-warp">
          <Header />
          <List todos={todos} />
          <Footer />
        </div>
      </div>
    )
  }
}
```

**>>List/index.jsx**

子组件通过this.props得到父组件传递过来的状态

通过循环遍历todos得到一个个todo，将他们传递给Item子组件

通过标签属性的形式，父组件List传递状态到子组件Item中

指定key 再展开todo传递给子组件

```javascript
export default class List extends Component {
  render() {
    const {todos} = this.props
    return (
      <ul className="todo-main">
        {
          todos.map((todo) => {
            return <Item key={todo.id} {...todo}/>
          })
        }
      </ul>
    )
  }
}
```

**>>Item/index.jsx**

子组件通过this.props得到父组件传递过来的每个todo的状态

动态渲染props中获取的状态 name 和 done

```javascript
export default class Item extends Component {
  render() {
    const { name, done } = this.props
    return (
      <li>
        <label>
          <input type="checkbox" defaultChecked={done}/>
          <span>{name}</span>
        </label>
        <button className="btn btn-danger" style={{display:'none'}}>删除</button>
      </li>
    )
  }
}
```


### 5.2 动态添加todo

子组件要向父组件 传递 得到的输入值

可以通过调用函数， 传递参数的形式 来传递状态

App.jsx

状态在父组件中，修改状态的操作就定义在父组件中

在父组件中定义一个addTodo函数，然后通过标签传递给子组件

addTodo函数接受一个参数，这个参数就是要接受的子组件的数据

通过这个参数，将子组件的数据传给父组件

```javascript
export default class App extends Component {
  // 用于添加一个todo，接受的参数是todo对象
  addTodo = (todoObj) => {
    // 获取原todos
    const { todos } = this.state
    // 追加一个todo
    const newTodos = [todoObj, ...todos]
    // 更新状态
    this.setState({ todos: newTodos })
  }
  render() {
    const  {todos} = this.state
    return (
      <div className="todo-container">
        <div className="todo-warp">
          <Header addTodo={this.addTodo} />
          <List todos={todos} />
          <Footer />
        </div>
      </div>
    );
  }
}
```

**>>Header/index.js**

生成唯一id的库

uuid

nanoid

npm install nanoid

父组件通过标签属性传递了一个函数给子组件，子组件可以通过this.props来调用函数

函数的参数，就是子组件要传递给父组件的数据

```javascript
export default class Header extends Component {
  handleKeyUp = (event) => {
    const {keyCode, target} = event
    if (keyCode !== 13) return
    if (target.value.trim() === '') {
      alert('输入不能为空')
      return
    }
    this.props.addTodo({
      id: nanoid(),
      name: target.value,
      done: false
    })
    target.value = ''
  }
  render() {
    return (
      <div className="todo-header">
        <input onKeyUp={this.handleKeyUp} type="text" placeholder="请输入你的任务名称，按回车键确认"/>
      </div>
    )
  }
}
```


## 5.3 鼠标悬浮高亮

定义一个mouse状态，用来 标识鼠标移入移出

通过mouse状态的改变，来改变style样式（背景颜色+删除按钮显示与隐藏）

**>>Item/index.js**
```javascript
export default class Item extends Component {
  // 标识鼠标移入移出
  state = {
    mouse: false
  }
  // 鼠标移入移出的回调
  handleMouse = (flag) => {
    return () => {
      this.setState({mouse: flag})
    }
  }
  render() {
    const { name, done } = this.props
    const {mouse} = this.state
    return (
      <li
        style={{ backgroundColor: mouse ? '#ddd' : 'white' }}
        onMouseEnter={this.handleMouse(true)}
        onMouseLeave={this.handleMouse(false)}
      >
        <label>
          <input type="checkbox" defaultChecked={done}/>
          <span>{name}</span>
        </label>
        <button className="btn btn-danger" style={{display: mouse?'block':'none'}}>删除</button>
      </li>
    )
  }
}
```


## 5.4 勾选 改变 状态

勾选前面的选中框，要改变到state中的数据

根据选中的框所属的todo的id找到数据，根据更改后done的值更新相应的done的值

**>>App.jsx**

在父组件中定义一个更新todo的函数，然后传递给子组件

根据拿到的id和done的值，来更新状态state中相应id数据的值
```javascript
export default class App extends Component {
  // 用于更新一个todo
  updateTodo = (id, done) => {
    const { todos } = this.state
    const newTodos = todos.map((todo) => {
      if (todo.id === id) {
        return {...todo, done: done}
      } else {
        return todo
      }
    })
    this.setState({todos: newTodos})
  }
  
  render() {
    const  {todos} = this.state
    return (
      <div className="todo-container">
        <div className="todo-warp">
          <Header addTodo={this.addTodo} />
          <List todos={todos} updateTodo={this.updateTodo}/>
          <Footer />
        </div>
      </div>
    );
  }
}
```


**>>List/index.jsx**

中转 从父组件App中传过来的函数，继续传给它的子组件Item，完成祖孙组件中的通信
```javascript
export default class List extends Component {
  render() {
    const {todos, updateTodo} = this.props
    return (
      <ul className="todo-main">
        {
          todos.map((todo) => {
            return <Item key={todo.id} {...todo} updateTodo={updateTodo}/>
          })
        }
      </ul>
    )
  }
}
```


**>>Item/index.jsx**

通过List中转终于拿到祖先组件App中的函数updateTodo

组件中定义onChange事件的回调函数handleCheck ，【高阶函数+柯里化】

在回调函数中返回传递过来的函数并传入参数
```javascript
export default class Item extends Component {
  // 勾选、取消勾选todo的回调
  handleCheck = (id) => {
    return (event) => {
      this.props.updateTodo(id, event.target.checked)
    }
  }

  render() {
    const { id, name, done } = this.props
    const {mouse} = this.state
    return (
      <li
        style={{ backgroundColor: mouse ? '#ddd' : 'white' }}
        onMouseEnter={this.handleMouse(true)}
        onMouseLeave={this.handleMouse(false)}
      >
        <label>
          <input type="checkbox" defaultChecked={done} onChange={ this.handleCheck(id) }/>
          <span>{name}</span>
        </label>
        <button className="btn btn-danger" style={{display:mouse?'block':'none'}}>删除</button>
      </li>
    )
  }
}
```

## 5.5 对props进行限制

类型及必要性设置

自行安装 prop-types 库 npm i prop-types
```javascript
import PropTypes from 'prop-types'
export default class Header extends Component {
  // 对接收的props进行类型以及必要性的限制
  static propTypes = {
    addTodo: PropTypes.func.isRequired
  }
}
```
```javascript
import PropTypes from 'prop-types'
export default class List extends Component {
  // 对接收的props进行类型以及必要性的限制
  static propTypes = {
      todos: PropTypes.array.isRequired,
      updateTodo: PropTypes.func.isRequired
  }
}
```

```javascript
import PropTypes from 'prop-types'
export default class Item extends Component {
  // 对接收的props进行类型以及必要性的限制
  static propTypes = {
    updateTodo: PropTypes.func.isRequired
  }
}
```

## 5.5 删除一个todo

选中一个todo，点击删除按钮，删除这个todo

**>>App.jsx**

因为状态数据在父组件中，所以删除todo的函数就定义在App中

然后将函数传递给子组件
```javascript
export default class App extends Component {
  // 用于删除一个todo
  deleteTodo = (id) => {
    const { todos } = this.state
    const newTodos = todos.filter((todo) => {
      return todo.id !== id
    })
    this.setState({todos:newTodos})
  }
  
  render() {
    const  {todos} = this.state
    return (
      <div className="todo-container">
        <div className="todo-warp">
          <Header addTodo={this.addTodo} />
          <List todos={todos} updateTodo={this.updateTodo} deleteTodo={this.deleteTodo} />
          <Footer />
        </div>
      </div>
    );
  }
```


**>>List/index.jsx**

中转拿到和函数继续传递

```javascript
export default class List extends Component {
  // 对接收的props进行类型以及必要性的限制
  static propTypes = {
    todos: PropTypes.array.isRequired,
    updateTodo: PropTypes.func.isRequired,
    deleteTodo: PropTypes.func.isRequired
  }
  render() {
    const {todos, updateTodo, deleteTodo} = this.props
    return (
      <ul className="todo-main">
        {
          todos.map((todo) => {
            return <Item key={todo.id} {...todo} updateTodo={updateTodo} deleteTodo={ deleteTodo }/>
          })
        }
      </ul>
    )
  }
}
```


**>>Item/index.jsx**
得到传递到的函数，将id作为函数参数传递给父组件

定义绑定点击事件 这次没用高阶函数，换了一种写法，效果是一样的
```javascript
export default class Item extends Component {
  // 对接收的props进行类型以及必要性的限制
  static propTypes = {
    updateTodo: PropTypes.func.isRequired,
    deleteTodo: PropTypes.func.isRequired
  }
  // 删除一个todo的回调
  handleDelete = (id) => {
    if (window.confirm(`确定删除嘛？`)) {
      this.props.deleteTodo(id)
    }
  }
  
  render() {
    const { id, name, done } = this.props
    const {mouse} = this.state
    return (
      <li
        style={{ backgroundColor: mouse ? '#ddd' : 'white' }}
        onMouseEnter={this.handleMouse(true)}
        onMouseLeave={this.handleMouse(false)}
      >
        <label>
          <input type="checkbox" defaultChecked={done} onChange={ this.handleCheck(id) }/>
          <span>{name}</span>
        </label>
        <button onClick={ () => this.handleDelete(id) } className="btn btn-danger" style={{display:mouse?'block':'none'}}>删除</button>
      </li>
    )
  }
}
```


##5.6 底部Footer

**>>App.jsx**

在App中将todos传给Footer

在App中定义全选和全不选的todos来更新状态

在App中定义清除所有已完成的todo

```javascript
export default class App extends Component {
  // 用于全选
  checkAll = (done) => {
    // 获取原来的todos
    const { todos } = this.state
    // 过滤数据
    const newTodos = todos.map((todo) => {
      return {...todo, done: done}
    })
    // 更新状态
    this.setState({todos: newTodos})
  }
  // 清除所有已经完成的
  clearAllDone = () => {
    const { todos } = this.state
    const newTodos = todos.filter((todo) => {
      return !todo.done
    })
    this.setState({todos: newTodos})
  }
  render() {
    const  {todos} = this.state
    return (
      <div className="todo-container">
        <div className="todo-warp">
          <Header addTodo={this.addTodo} />
          <List todos={todos} updateTodo={this.updateTodo} deleteTodo={this.deleteTodo} />
          <Footer todos={todos} checkAll={this.checkAll} clearAllDone={this.clearAllDone} />
        </div>
      </div>
    );
  }
}
```

**>>Footer/index.jsx**
拿到todos

用来计算两个数据doneCount和total，显示在页面中

定义两个回调函数handleCheckAll和handleClearAllDone

再从父组件接收两个函数然后调用
```javascript
export default class Footer extends Component {
  // 全选
  handleCheckAll = (event) => {
    this.props.checkAll(event.target.checked)
  }
  // 清除所有已完成的回调
  handleClearAllDone = () => {
    this.props.clearAllDone()
  }
  render() {
    const { todos } = this.props
    // 计算已完成
    const doneCount = todos.reduce((pre, todo) => { return pre + (todo.done ? 1: 0) }, 0)
    // 计算总数
    const total = todos.length
    return (
      <div className="todo-footer">
      <label>
          <input type="checkbox" onChange={this.handleCheckAll} checked={doneCount === total && total !== 0 ? true: false }/>
      </label>
      <span>
          <span>已完成{ doneCount }</span> / 全部{total}
      </span>
      <button onClick={this.handleClearAllDone} className="btn btn-danger">清除已完成任务</button>
    </div>
    )
  }
}
```


# 6. 总结

拆分组件、实现静态组件，注意：className、style的写法

动态初始化列表，如何确定将数据放在哪个组件的state中？

某个组件使用：放在其 自身 的state中

某些组件使用：放在他们共同的 父组件 state中（官方称此操作为：状态提升）


关于父子之间通信：

【父组件】给【子组件】传递数据：通过props传递

【子组件】给【父组件】传递数据：通过props传递，要求父提前给子传递一个函数


注意defaultChecked （只在第一次指定的时候有作用，之后就没作用了）和 checked的区别，类似的还有：defaultValue 和 value
状态在哪里，操作状态的方法就在哪里

![image](https://user-images.githubusercontent.com/117837871/220587169-d8c3072c-e800-46c0-8db2-83abd26f2911.png)

![image](https://user-images.githubusercontent.com/117837871/220587280-1a81ccc3-a9b7-4012-aeed-b8959acf65a0.png)

![image](https://user-images.githubusercontent.com/117837871/220587310-7b5ec9e9-8c6b-4929-b215-130d49d0e17a.png)

注意defaultChecked （只在第一次指定的时候有作用，之后就没作用了）和 checked的区别，类似的还有：defaultValue 和 value
# 用户搜索页面与配置代理

今天我们使用React做一个需要发起ajax请求的小demo（github用户搜索页面），我们先使用axios实现，最后再实现一个fetch版本的。

这中间我们还会在React中配置代理来解决跨域问题，还会使用消息订阅与发布模式改进我们的代码。

## 1. 理解
之前也学习过ajax和axios，可以先看看这两个笔记复习一下ajax

[【Ajax】HTTP相关问题-GET-POST-XHR使用-jQuery中的ajax-跨域-同源-jsonp-cors](https://juejin.cn/post/6999604180432191519)

[【Axios】使用json-server 搭建REST API - 使用axios - 自定义axios - 取消请求 - 拦截器](https://juejin.cn/post/7015487317582299144)


### 1.1. 前置说明

React本身只关注于界面, 并不包含发送**ajax**请求的代码

前端应用需要通过ajax请求与后台进行交互(json数据)

React应用中需要集成第三方ajax库(或自己封装)

### 1.2. 常用的ajax请求库

jQuery: 比较重, 如果需要另外引入不建议使用

axios: 轻量级, 建议使用

    1.封装XmlHttpRequest对象的ajax

    2.promise风格

    3.可以用在浏览器端和node服务器端

## 2. axios

安装**npm install axios**

### 2.1. 文档

Github.com/axios/axios

### 2.2. 相关API

更多细节可以参考这个笔记的内容 [【axios】使用json-server 搭建REST API - 使用axios - 自定义axios - 取消请求 - 拦截器](https://blog.csdn.net/weixin_44972008/article/details/114368528)


## 3. React中配置代理解决跨域问题

### 3.1 配置代理方法

解决跨域问题，在React开启中间代理

在项目中的package.json中，最后加上一行"proxy": "http://loaclhost:5000" 写到端口号

然后重启脚手架

再次发送请求的时候就直接写自己的3000端口

3000端口有的资源直接请求3000端口的，3000端口没有的资源就请求代理设置的5000端口

在package.json中追加如下配置

```javascript
"proxy":"http://localhost:5000"
```

说明：

    优点：配置简单，前端请求资源时可以不加任何前缀。

    配置多个代理。

    工作方式：上述方式配置代理，当请求了3000不存在的资源时，那么该请求会转发给5000 （优先匹配前端资源）


### 3.2 配置多个代理方法

配置多个代理，不在 package.json 配置

    第一步：创建代理配置文件

在src下创建配置文件：src/setupProxy.js

    编写setupProxy.js配置具体代理规则：

```javascript
const proxy = require('http-proxy-middleware')

module.exports = function(app) {
  app.use(
    proxy('/api1', {  //api1是需要转发的请求(所有带有/api1前缀的请求都会转发给5000)
      target: 'http://localhost:5000', //配置转发目标地址(能返回数据的服务器地址)
      changeOrigin: true, //控制服务器接收到的请求头中host字段的值
      /*
      	changeOrigin设置为true时，服务器收到的请求头中的host为：localhost:5000
      	changeOrigin设置为false时，服务器收到的请求头中的host为：localhost:3000
      	changeOrigin默认值为false，但我们一般将changeOrigin值设为true
      */
      pathRewrite: {'^/api1': ''} //去除请求前缀，保证交给后台服务器的是正常请求地址(必须配置)
    }),
    proxy('/api2', { 
      target: 'http://localhost:5001',
      changeOrigin: true,
      pathRewrite: {'^/api2': ''}
    })
  )
}
```

说明：
1.优点：可以配置多个代理，可以灵活的控制请求是否走代理。

2.缺点：配置繁琐，前端请求资源时必须加前缀。

## 4. 案例—github用户搜索

之前用Vue也做过这个案例，可以对比着学习 [【Vue】高级系列（七）Vue-cli配置代理 - Ajax实战-demo3-GitHub用户查询-axios-pubsub](https://blog.csdn.net/weixin_44972008/article/details/113992327)

### 4.1 效果

请求地址: https://api.github.com/search/users?q=xxxxxx

https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/e17bce649e774e089e6b423830c2a28e~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp

### 4.2 React 实现

#### 4.2.1 静态页面拆分实现


**>>App.jsx**

```javascript
import React, { Component } from 'react'
import Search from './Search'
import Users from './Users'

export default class App extends Component {
  render() {
    return (
      <div className="container">
        <Search />
        <Users />
    </div>
    )
  }
}
```

**>>Search/index.js**

```javascript
import React, { Component } from 'react'

export default class Search extends Component {
  render() {
    return (
      <section className="jumbotron">
      <h3 className="jumbotron-heading">搜索Github用户</h3>
      <div>
          <input type="text" placeholder="请输入你要搜索的用户名" />&nbsp;
          <button>搜索</button>
      </div>
      </section>
    )
  }
}
```
**>>User/index.jsx**

```javascript
import React, { Component } from 'react'
import './index.css'

export default class Users extends Component {
  render() {
    return (
      <div className="row">
        <div className="card">
          <a rel="noreferrer" href="https://github.com/reactjs" target="_blank">
              <img alt="avatar" src="https://avatars.githubusercontent.com/u/6412038?v=3" style={{ 'width': '100px' }}/>
          </a>
          <p className="card-text">reactjs</p>
        </div>
        <div className="card">
          <a rel="noreferrer" href="https://github.com/reactjs" target="_blank">
            <img alt="avatar" src="https://avatars.githubusercontent.com/u/6412038?v=3" style={{ 'width': '100px' }}/>
          </a>
          <p className="card-text">reactjs</p>
        </div>
        <div className="card">
          <a rel="noreferrer" href="https://github.com/reactjs" target="_blank">
            <img alt="avatar" src="https://avatars.githubusercontent.com/u/6412038?v=3" style={{ 'width': '100px' }}/>
          </a>
          <p className="card-text">reactjs</p>
        </div>
        <div className="card">
          <a rel="noreferrer" href="https://github.com/reactjs" target="_blank">
            <img alt="avatar" src="https://avatars.githubusercontent.com/u/6412038?v=3" style={{ 'width': '100px' }}/>
          </a>
          <p className="card-text">reactjs</p>
        </div>
        <div className="card">
          <a rel="noreferrer" href="https://github.com/reactjs" target="_blank">
            <img alt="avatar" src="https://avatars.githubusercontent.com/u/6412038?v=3" style={{ 'width': '100px' }}/>
          </a>
          <p className="card-text">reactjs</p>
        </div>
      </div>
    )
  }
}
```

**>>User/index.css**
```css
.album {
  min-height: 50rem; /* Can be removed; just added for demo purposes */
  padding-top: 3rem;
  padding-bottom: 3rem;
  background-color: #f7f7f7;
}

.card {
  float: left;
  width: 33.333%;
  padding: .75rem;
  margin-bottom: 2rem;
  border: 1px solid #efefef;
  text-align: center;
}

.card > img {
  margin-bottom: .75rem;
  border-radius: 100px;
}

.card-text {
  font-size: 85%;
}
```



#### 4.2.2 动态交互实现

由于github访问失败，可以伪造一个服务器返回一些固定的结果，让用户体验更佳 使用express搭建一个服务器

**>>serve.js**

```javascript
const express = require("express")
const axios = require("axios")
const app = express()

/*
  请求地址： http://localhost:3000/search/users?q=aa

  后台路由
    key： /search/users
    value： function () {}
*/
app.get("/search/users", function (req, res) {
  const {q} = req.query
  axios({
    url: 'https://api.github.com/search/users',
    params: {q}
  }).then(response => {
    res.json(response.data)
  })
})

app.get("/search/users2", function (req, res) {
  res.json({
    items: [
      {
        login: "yyx990803",
        html_url: "https://github.com/yyx990803",
        avatar_url:
          "https://avatars3.githubusercontent.com/u/499550?s=460&u=de41ec9325e8a92e281b96a1514a0fd1cd81ad4a&v=4",
        id: 1,
      },
      {
        login: "ruanyf",
        html_url: "https://github.com/ruanyf",
        avatar_url: "https://avatars2.githubusercontent.com/u/905434?s=460&v=4",
        id: 2,
      },
      {
        login: "yyx9908032",
        html_url: "https://github.com/yyx990803",
        avatar_url:
          "https://avatars3.githubusercontent.com/u/499550?s=460&u=de41ec9325e8a92e281b96a1514a0fd1cd81ad4a&v=4",
        id: 3,
      },
      {
        login: "ruanyf2",
        html_url: "https://github.com/ruanyf",
        avatar_url: "https://avatars2.githubusercontent.com/u/905434?s=460&v=4",
        id: 4,
      },
      {
        login: "yyx9908033",
        html_url: "https://github.com/yyx990803",
        avatar_url:
          "https://avatars3.githubusercontent.com/u/499550?s=460&u=de41ec9325e8a92e281b96a1514a0fd1cd81ad4a&v=4",
        id: 5,
      },
      {
        login: "ruanyf3",
        html_url: "https://github.com/ruanyf",
        avatar_url: "https://avatars2.githubusercontent.com/u/905434?s=460&v=4",
        id: 6,
      },
      {
        login: "yyx9908034",
        html_url: "https://github.com/yyx990803",
        avatar_url:
          "https://avatars3.githubusercontent.com/u/499550?s=460&u=de41ec9325e8a92e281b96a1514a0fd1cd81ad4a&v=4",
        id: 7,
      },
      {
        login: "ruanyf4",
        html_url: "https://github.com/ruanyf",
        avatar_url: "https://avatars2.githubusercontent.com/u/905434?s=460&v=4",
        id: 8,
      },
      {
        login: "yyx9908035",
        html_url: "https://github.com/yyx990803",
        avatar_url:
          "https://avatars3.githubusercontent.com/u/499550?s=460&u=de41ec9325e8a92e281b96a1514a0fd1cd81ad4a&v=4",
        id: 9,
      },
    ],
  });
});



app.listen(5000, "localhost", (err) => {
  if (!err){
  	console.log("服务器启动成功")
  	console.log("请求github真实数据请访问：http://localhost:5000/search/users")
  	console.log("请求本地模拟数据请访问：http://localhost:5000/search/users2")
  } 
  else console.log(err);
})
```

在这里插入图片描述

**src/setupProxy.js**

设置代理服务器解决跨域问题src/setupProxy.js

```javascript
const proxy = require('http-proxy-middleware')

module.exports = function(app) {
  app.use(
    proxy('/api1', {  //api1是需要转发的请求(所有带有/api1前缀的请求都会转发给5000)
      target: 'http://localhost:5000', //配置转发目标地址(能返回数据的服务器地址)
      changeOrigin: true, //控制服务器接收到的请求头中host字段的值
      pathRewrite: {'^/api1': ''} //去除请求前缀，保证交给后台服务器的是正常请求地址(必须配置)
    })
  )
}

// 【补充】连续解构赋值
let obj = {a:{b:{c:1}}}
console.log(a.b.c) // 1
const {a:{b:{c}}} = obj
console.log(c) // 1

let obj2 = {a:{b:1}}
const {a:{b:data}} = obj2 // 重命名
console.log(data) // 1
```

**>>App.jsx**

将状态数据定义在App中 操作状态的方法放在App中
```javascript
export default class App extends Component {
  state = {
    users: []
  }
  saveUsers = (users) => {
    this.setState({ users })
  }
  render() {
    const {users} = this.state
    return (
      <div className="container">
        <Search saveUsers={this.saveUsers} />
        <Users users={users} />
    </div>
    )
  }
}
```

**>>Search/index/jsx**

```javascript
export default class Search extends Component {
  search = () => {
    // 获取用户输入(连续解构赋值+重命名)
    const {keyWordElement: {value: keyWord}} = this
    // console.log(keyWord)
    // 发送网络请求
    axios.get(`/api1/search/users?q=${keyWord}`).then(
      response => {
        console.log('成功')
        this.props.saveUsers(response.data.items)
      },
      error => {console.log('失败',error)}
    )
  }
  render() {
    return (
      <section className="jumbotron">
      <h3 className="jumbotron-heading">搜索Github用户</h3>
      <div>
          <input ref={c => this.keyWordElement = c} type="text" placeholder="请输入你要搜索的用户名" />&nbsp;
          <button onClick={this.search}>搜索</button>
      </div>
      </section>
    )
  }
}
```

**>>Users/index.jsx**

```javascript
export default class Users extends Component {
  render() {
    return (
      <div className="row">
        {
          this.props.users.map((userObj) => {
            return (
              <div key={userObj.id} className="card">
                <a rel="noreferrer" href={userObj.html_url} target="_blank">
                    <img alt="avatar" src={userObj.avatar_url} style={{ 'width': '100px' }}/>
                </a>
                <p className="card-text">{userObj.login}</p>
              </div>
            )
          })
        }
      </div>
    )
  }
}
```
效果展示

在这里插入图片描述

#### 4.2.3 优化用户体验

在Users组件中，应该不止只有用户列表页面，应该还有

    1.欢迎使用界面【第一次打开页面】

    2.搜索加载页面【点击按钮发送请求和接收到响应之间显示】

    3.搜索失败页面【请求失败显示】

有四种不同的显示，那就需要不同的状态state来控制

```javascript
// 初始化状态
state = { 
  users: [], // users初始值
  isFirst: true, // 是否第一次打开页面
  isLoading: false, // 标识是否处于加载中
  err:'' // 请求失败的消息
}
```

**>>App.jsx**
```javascript
export default class App extends Component {
  // 初始化状态
  state = { 
    users: [], // users初始值
    isFirst: true, // 是否第一次打开页面
    isLoading: false, // 标识是否处于加载中
    err:'' // 请求失败的消息
  }
  // saveUsers = (users) => {
  //   this.setState({ users })
  // }
  // 更新App的state
  updateAppState = (stateObj) => {
    this.setState(stateObj)
  }
  render() {
    return (
      <div className="container">
        <Search updateAppState={this.updateAppState} />
        <Users {...this.state} />
    </div>
    )
  }
}
```

**>>Search/index/jsx**

```javascript
export default class Search extends Component {
  search = () => {
    // 获取用户输入(连续解构赋值+重命名)
    const {keyWordElement: {value: keyWord}} = this
    // console.log(keyWord)
    // 发送请求前通知App更新状态
    this.props.updateAppState({
      isFirst: false,
      isLoading: true
    })
    // 发送网络请求
    axios.get(`/api1/search/users?q=${keyWord}`).then(
      response => {
        // console.log('成功')
        // 请求成功，通知App更新状态
        this.props.updateAppState({isLoading: false, users: response.data.items})
        // this.props.saveUsers(response.data.items)
      },
      error => {
        // console.log('失败', error)
        // 请求失败，通知App更新状态
        this.props.updateAppState({isLoading: false, err: error.message})
      }
    )
  }
  render() {
    return (
      <section className="jumbotron">
      <h3 className="jumbotron-heading">搜索Github用户</h3>
      <div>
          <input ref={c => this.keyWordElement = c} type="text" placeholder="请输入你要搜索的用户名" />&nbsp;
          <button onClick={this.search}>搜索</button>
      </div>
      </section>
    )
  }
}
```

**>>Users/index.jsx**

```javascript
export default class Users extends Component {
  render() {
    const {users, isFirst, isLoading, err} = this.props
    return (
      <div className="row">
        {
          isFirst ? <h2>欢迎使用，请输入关键字，随后点击搜索</h2> :
          isLoading ? <h2>Loading...</h2> :
          err ? <h2 style={{color: 'red'}}>{err}</h2> :
          users.map((userObj) => {
            return (
              <div key={userObj.id} className="card">
                <a rel="noreferrer" href={userObj.html_url} target="_blank">
                    <img alt="avatar" src={userObj.avatar_url} style={{ 'width': '100px' }}/>
                </a>
                <p className="card-text">{userObj.login}</p>
              </div>
            )
          })
        }
      </div>
    )
  }
}
```

效果展示
在这里插入图片描述

## 5. 消息订阅-发布机制

前面案例中，兄弟组件之间的通信总是要借助父组件才行 现在介绍消息订阅-发布机制来进行兄弟组件之间通信

介绍PubSubJS库

[PubSubJS](https://github.com/mroderick/PubSubJS)

1.工具库: PubSubJS

2.下载: **npm install pubsub-js**在这里插入图片描述

使用 在【接收】数据的组件中【订阅】消息

```javascript
import PubSub from 'pubsub-js' //引入（包名的命名规范中不能出现字母）

PubSub.subscribe('delete', function(data){ }); // 订阅

PubSub.publish('delete', data) // 发布消息 携带数据
```

在案例中使用

Users组件【接收】数据，所以Users组件【订阅】消息 Search组件 将数据发送出去，【发布】消息

**>>App.js**

```javascript
export default class App extends Component {
  render() {
    return (
      <div className="container">
        <Search />
        <Users />
    </div>
    )
  }
}
```

**>>Users/index.jsx**

User组件中用状态数据state，状态定义在这里，在这里订阅消息 Search组件改变状态数据，在这里发布消息
```javascript
export default class Users extends Component {
  // 初始化状态
  state = { 
    users: [], // users初始值
    isFirst: true, // 是否第一次打开页面
    isLoading: false, // 标识是否处于加载中
    err:'' // 请求失败的消息
  }
  componentDidMount() {
    // 订阅消息
    PubSub.subscribe('ykyk', (_, data) => {
      this.setState(data)
    })
  }
  render() {
    const {users, isFirst, isLoading, err} = this.state
    return (
      <div className="row">
        {
          isFirst ? <h2>欢迎使用，请输入关键字，随后点击搜索</h2> :
          isLoading ? <h2>Loading...</h2> :
          err ? <h2 style={{color: 'red'}}>{err}</h2> :
          users.map((userObj) => {
            return (
              <div key={userObj.id} className="card">
                <a rel="noreferrer" href={userObj.html_url} target="_blank">
                    <img alt="avatar" src={userObj.avatar_url} style={{ 'width': '100px' }}/>
                </a>
                <p className="card-text">{userObj.login}</p>
              </div>
            )
          })
        }
      </div>
    )
  }
}
```

**>>Search/index.jsx**

Search组件改变状态数据，在这里发布消息【一改变状态，就发布消息】

```javascript
export default class Search extends Component {
  search = () => {
    const {keyWordElement: {value: keyWord}} = this
    // 发送请求前通知Users更新状态
    // this.props.updateAppState({isFirst: false,isLoading: true})
    PubSub.publish('ykyk', {isFirst: false,isLoading: true})
    // 发送网络请求
    axios.get(`/api1/search/users?q=${keyWord}`).then(
      response => {
        // 请求成功，通知Users更新状态
        PubSub.publish('ykyk', {isLoading: false, users: response.data.items})
        // this.props.updateAppState({isLoading: false, users: response.data.items})
      },
      error => {
        // 请求失败，通知Users更新状态
        PubSub.publish('ykyk', {isLoading: false, err: error.message})
        // this.props.updateAppState({isLoading: false, err: error.message})
      }
    )
  }
  render() {
    return (
      <section className="jumbotron">
      <h3 className="jumbotron-heading">搜索Github用户</h3>
      <div>
          <input ref={c => this.keyWordElement = c} type="text" placeholder="请输入你要搜索的用户名" />&nbsp;
          <button onClick={this.search}>搜索</button>
      </div>
      </section>
    )
  }
}
```

6. Fetch

Axios在前端是对xhr的封装 而Fetch是内置的网络请求方法，不需要单独下载安装

6.1 文档

github.github.io/fetch/

【相关博文】传统 Ajax 已死，Fetch 永生


6.2 特点

fetch: 原生函数，不再使用XmlHttpRequest对象提交ajax请求

老版本浏览器可能不支持


6.3 实例演示

Search/index.jsx

优化前

```javascript
export default class Search extends Component {
	search = async()=>{
		//获取用户的输入(连续解构赋值+重命名)
		const {keyWordElement:{value:keyWord}} = this
		//发送请求前通知List更新状态
		PubSub.publish('ykyk',{isFirst:false,isLoading:true})
		
		//发送网络请求---使用fetch发送（未优化）
		fetch(`/api1/search/users2?q=${keyWord}`).then(
			response => {
				console.log('联系服务器成功了');
				return response.json()
			},
			error => {
				console.log('联系服务器失败了',error);
        //返回初始化状态的promise值,不再往下走。
				return new Promise(()=>{})
			}
		).then(
			response => {console.log('获取数据成功了',response);},
			error => {console.log('获取数据失败了',error);}
		)
	}
}
```
优化后

```javascript
export default class Search extends Component {
	search = async()=>{
		//获取用户的输入(连续解构赋值+重命名)
		const {keyWordElement:{value:keyWord}} = this
		//发送请求前通知List更新状态
		PubSub.publish('ykyk',{isFirst:false,isLoading:true})

		//发送网络请求---使用fetch发送（优化）
		try {
			const response = await fetch(`/api1/search/users2?q=${keyWord}`)
			const data = await response.json()
			// console.log(data);
			PubSub.publish('ykyk',{isLoading:false, users:data.items})
		} catch (error) {
			// console.log('请求出错',error);
			PubSub.publish('ykyk',{isLoading:false, err:error.message})
		}
	}
}
```


7. 总结

设计状态时要考虑全面，例如带有网络请求的组件，要考虑请求失败怎么办。

ES6小知识点：解构赋值+重命名

let obj = {a:{b:1}}

const {a} = obj; //传统解构赋值

const {a:{b}} = obj; //连续解构赋值

const {a:{b:value}} = obj; //连续解构赋值+重命名

消息订阅与发布机制

先订阅，再发布（理解：有一种隔空对话的感觉）

适用于任意组件间通信

要在组件的componentWillUnmount中取消订阅

fetch发送请求（关注分离的设计思想）

```javascript
try {
	const response= await fetch(`/api1/search/users2?q=${keyWord}`)
	const data = await response.json()
	console.log(data);
} catch (error) {
	console.log('请求出错',error);
}
```

【React】SPA - 路由机制 - react-router5 - 基本路由 - 嵌套路由 - 传递参数 - 路由跳转


# 1. 相关理解

## 1.1. SPA的理解

单页Web应用（single page web application，SPA）

整个应用只有一个完整的页面。

点击页面中的链接不会刷新页面，只会做页面的局部更新。

数据都需要通过ajax请求获取, 并在前端异步展现。

## 1.2. 路由的理解

### 1.2.1 什么是路由?

一个路由就是一个映射关系(key: value)

key为路径, value可能是function或component

### 1.2.2 路由分类


* 1. 后端路由

  * 理解： value是function, 用来处理客户端提交的请求。

  * 注册路由： router.get(path, function(req, res))

  * 工作过程：当node接收到一个请求时, 根据请求路径找到匹配的路由, 调用路由中的函数来处理请求, 返回响应数据


* 2. 前端路由

  * 浏览器端路由，value是component，用于展示页面内容。

  * 注册路由: <Route path="/test" component={Test}>

  * 工作过程：当浏览器的path变为/test时, 当前路由组件就会变为Test组件

  * 主要是通过操作BOM中的history来操作路径

## 1.3. react-router-dom 的理解

* React的一个插件库。

* 专门用来实现一个SPA应用。

* 基于React的项目基本都会用到此库。


# 2. react-router-dom相关API

## 2.1. 内置组件

```javascript
<BrowserRouter>
<HashRouter>
<Route>
<Redirect>
<Link>
<NavLink>
<Switch>
```

## 2.2. 其它

history 对象

match 对象

withRouter 函数


# 3. 基本路由使用

## 3.1. 效果

[在这里插入图片描述](https://p3-juejin.byteimg.com/tos-cn-i-k3u1fbpfcp/34f6957bbd4f46efac620ff7d66003a4~tplv-k3u1fbpfcp-zoom-in-crop-mark:4536:0:0:0.awebp)

## 3.2. 准备

下载react-router-dom: npm install react-router-dom

引入bootstrap.css: <link rel="stylesheet" href="/css/bootstrap.css">

## 3.3 路由的基本使用

1.明确好界面中的导航区、展示区

2.导航区的a标签改为Link标签 ```<Link to="/xxxxx">Demo</Link>```//to里面尽量都小写

3.展示区写Route标签进行路径的匹配 ```<Route path='/xxxx' component={Demo}/>```

4.```<App>```的最外侧包裹了一个```<BrowserRouter>```或```<HashRouter>```

(BrowserRouter 将会监听 URL 的变化，当 URL 变更时，它将使浏览器显示相应的页面；所以要在最外侧包裹一个)


## 3.4 实现

**>>Index.js**

这里用一个路由器标签将整个App包起来，保证使用的是同一个路由器这里使用BrowserRouter
```javascript
//引入react核心库
import React from 'react'
//引入ReactDOM
import ReactDOM from 'react-dom'
//
import {BrowserRouter} from 'react-router-dom'
//引入App
import App from './App'

ReactDOM.render(
    <BrowserRouter>
        <App/>
    </BrowserRouter>,
    document.getElementById('root')
)
```

**>>App.jsx**

```javascript
import React, { Component } from 'react'
import { Link,Route } from 'react-router-dom'
import Home from './Home'
import About from './About'

export default class App extends Component {
  render() {
    return (
      <div>
      <div className="row">
        <div className="col-xs-offset-2 col-xs-8">
          <div className="page-header"><h2>React Router Demo</h2></div>
        </div>
      </div>
      <div className="row">
        <div className="col-xs-2 col-xs-offset-2">
          <div className="list-group">
            {/* 原生html中，靠<a>跳转不同的页面 */}
            {/* <a className="list-group-item" href="./about.html">About</a>
            <a className="list-group-item active" href="./home.html">Home</a> */}

            {/* 在React中靠路由链接实现切换组件--编写路由链接 */}
            <Link className="list-group-item" to="/about">About</Link>
            <Link className="list-group-item" to="/home">Home</Link>
          </div>
        </div>
        <div className="col-xs-6">
          <div className="panel">
              <div className="panel-body">
                {/* 注册路由 */}
                <Route path='/about' component={About} />
                <Route path='/home' component={Home} />
            </div>
          </div>
        </div>
      </div>
    </div>
    )
  }
}
```

## 3.5 路由组件与一般组件的区别

```#号后面的东西不作为数据发送给服务器```

一、写法不同

* 一般组件：

```javascript
<Demo/>
```

* 路由组件：

```javascript
<Route path="/demo" component={Demo}/>
```

二、存放位置不同

* 一般组件：components

* 路由组件：pages

三、接收到的props不同

* 一般组件：写组件标签时传递了什么，就能收到什么

* 路由组件：接收到三个固定的属性

```javascript
history: 

  go: ƒ go(n)

  goBack: ƒ goBack() 

  goForward: ƒ goForward() 

  push: ƒ push(path, state) 

  replace: ƒ replace(path, state) 


location:

  pathname: "/about"

  search: ""

  state: undefined


match:

  url: "/about"

  params: {}

  path: "/about"
```



## 3.6 NavLink与封装NavLink

NavLink可以实现路由链接的高亮，通过activeClassName属性指定样式名，默认是"active"

```javascript
<NavLink activeClassName="demo" className="list-group-item" to="/home">Home</NavLink>
```

可以自己封装一个NavLink【一般组件】

```javascript
import React, { Component } from 'react'
import {NavLink} from 'react-router-dom'

export default class MyNavLink extends Component {
  render() {
    // console.log(this.props);
    return (
      <NavLink activeClassName="demo" className="list-group-item" {...this.props} />
    )
  }
}
```
标签体内容是特殊的标签属性通过this.props.children可以获取标签体内容

使用
```javascript
<MyNavLink to="/about">About</MyNavLink>

<MyNavLink to="/home">Home</MyNavLink>
```



## 3.7 Switch的使用

* 通常情况下，path和component是一一对应的关系。```<Route path='/about' component={About} />```

* **Switch**可以提高路由匹配效率(单一匹配)。

这样只要匹配到了第一个就不会再往下匹配了

引入switch
```javascript
<Switch>
  <Route path="/about" component={About}/>
  <Route path="/home" component={Home}/> 
  <Route path="/home" component={Test}/>
</Switch>
```

# 例子：
```javascript
import React,{Component} from 'react';
import {HashRouter as Router,Route,Link,Switch } from 'react-router-dom';
import Main from './Main';
import About from './About';
import Topic from './Topic';
class Home extends Component {
    constructor(props) {
        super(props);
        this.state = {  };
    }
    render() {
        return (
            <Router>
                <div>
                <ul>
                    <li>
                        <Link to="/">main</Link>
                    </li>
                    <li>
                        <Link to="/about">about</Link>
                    </li>
                    <li>
                        <Link to="/topic">topic</Link>
                    </li>
                </ul>
                <hr />
                {/* {this.props.children} */}
                </div>
                {/* Switch匹配到第一个路由就不会继续匹配了,
                如果不加Route 里不加 exact，那么凡是Link里面 to 的路径包含了/，
                那么就会被匹配到，于是Switch就不继续匹配下去
                
                */}
                <Switch>
                    <Route  exact path="/" component={Main}></Route>
                    <Route  path="/about" component={About}></Route>
                    <Route  path="/topic" component={Topic}></Route>
                </Switch>
            </Router>
            
        );
    }
}

export default Home;
```

## 3.8 解决多级路径刷新页面样式丢失的问题

【Pulbic文件夹就是根目录/】

《解决方案》

* public/index.html 中 引入样式时不写 ./ 写 / （常用）【绝对路径】

* public/index.html 中 引入样式时不写 ./ 写 %PUBLIC_URL% （常用）

* 使用HashRouter

问题原因：多级路径下，加载样式时，使用相对路径，在刷新时将多级路由也考虑在内

// 如下，样式路径 './' 导致加载资源时，需要参考当前路径，因此多级路由会影响资源的加载
 <link rel="stylesheet" href="./test.css" />

解决的三种方法：
使用 绝对路径
public/index.html 中 引入样式时不写 ./ 写 / （常用）
 // 加载 根目录下的 test.css ，与当前路由无关
 <link rel="stylesheet" href="/test.css" />

使用 %PUBLIC_URL%（此方法只有在react中有效）
public/index.html 中 引入样式时不写 ./ 写 %PUBLIC_URL% （常用）
 // 加载 public 文件夹下的 test.css ，与当前路由无关
 <link rel="stylesheet" href="%PUBLIC_URL%/test.css" />

原理：使用绝对路径，即固定了是public下的test.css，并不会被变动。

使用HashRouter
ReactDOM.render(
    <HashRouter>
        <App />
    </HashRouter>
    , document.getElementById('root'))

原理：因为 hash 是不会改变路径的，也不会包含在请求URL中，因此不会影响相对路径

总结：
样式丢失的原因是，加载资源时使用相对路径，而相对路径又会参考当前路由路径，因此导致加载不到资源，解决办法则是使用绝对路径等，让其加载资源时不再参考路由路径。

## 3.9 路由的严格匹配与模糊匹配

默认使用的是模糊匹配（简单记：【输入的路径】必须包含要【匹配的路径】，且顺序要一致）
开启严格匹配：<Route exact={true} path="/about" component={About}/>简写<Route exact path="/about" component={About}/>
严格匹配不要随便开启，需要再开，有些时候开启会导致无法继续匹配二级路由

## 3.10 Redirect的使用【重定向】
一般写在所有路由注册的最下方，当所有路由都无法匹配时，跳转到Redirect指定的路由

具体编码：
```javascript
<Switch>
    <Route path="/about" component={About}/>
    <Route path="/home" component={Home}/>
    <Redirect to="/about"/>
</Switch>
```

# 4. 嵌套路由使用

## 4.1 效果

在这里插入图片描述

## 4.2 注意
注册子路由时要写上父路由的path值

路由的匹配是按照注册路由的顺序进行的

## 4.3 实现

**>>Home/index.jsx**

```javascript
import React, { Component } from 'react'
import { Route, NavLink,Redirect,Switch } from 'react-router-dom'
import News from './News'
import Message from './Message'

export default class Home extends Component {
  render() {
    return (
      <div>
        <h3>我是Home的内容</h3>
        <div>
          <ul className="nav nav-tabs">
            <li>
              <NavLink className="list-group-item" to="/home/news">News</NavLink>
            </li>
            <li>
              <NavLink className="list-group-item" to="/home/message">Message</NavLink>
            </li>
          </ul>
          <Switch>
            <Route path='/home/news' component={News} />
            <Route path='/home/message' component={Message} />
            <Redirect to='/home/news' />
          </Switch>
        </div>
      </div>
    )
  }
}
```

# 5. 向路由组件传递参数数据

## 5.1 效果

在这里插入图片描述

## 5.2 具体方法

方法1. params参数
路由链接(携带参数)：<Link to='/demo/test/tom/18'}>详情</Link>
注册路由(声明接收)：<Route path="/demo/test/:name/:age" component={Test}/>
接收参数：this.props.match.params

**>>Message/index.jsx**
```javascript
import React, { Component } from 'react'
import { Link, Route } from 'react-router-dom';
import Detail from './Detail';

export default class Message extends Component {
  state = {
    messageArr: [
      { id: '01', title: '消息1' },
      { id: '02', title: '消息2' },
      { id: '03', title: '消息3' },
    ]
  }
  render() {
    const { messageArr } = this.state;
    return (
      <div>
        <ul>
          {
            messageArr.map((msgObj) => {
              return (
                <li key={msgObj.id}>
                  {/* 向路由组件传递params参数 */}
                  <Link to={`/home/message/detail/${msgObj.id}/${msgObj.title}`}>{msgObj.title}</Link>
                </li>
              )
            })
          }
        </ul>
        <hr />
        {/* 声明接收params参数 */}
        <Route path="/home/message/detail/:id/:title" component={Detail}/>
      </div>
    )
  }
}
```

**>>Detail/index.jsx**

在这里插入图片描述
```javascript
import React, { Component } from 'react'

export default class Detail extends Component {
  state = {
    detailData : [
      { id: '01', content: '你好啊' },
      { id: '02', content: '还不错鸭' },
      { id: '03', content: '显示我吧' }
    ]
  }
  render() {
    console.log(this.props)
    // 接收params参数
    const { id, title } = this.props.match.params
    const findResult= this.state.detailData.find((dataObj) => {
      return dataObj.id === id
    })
    return (
      <div>
        <ul>
          <li>ID: {id }</li>
          <li>Title: {title }</li>
          <li>Content: { findResult.content}</li>
        </ul>
      </div>
    )
  }
}
```