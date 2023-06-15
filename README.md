# React框架

## 第一章：React基础

### ReactJS简介

+ React 起源于 Facebook 的内部项目，因为该公司对市场上所有 JavaScript MVC 框架，都不满意，就决定自己写一套，用来架设 Instagram 的网站。做出来以后，发现这套东西很好用，**就在2013年5月开源了**。
+ 官方对react的定位是：用于构建用户界面的 JavaScript 库
+ 轻量级前端框架，支持JSX（JavaScript XML）语法，jsx是js内定义的一套XML语法，最终被解析成js。在JSX中可以将HTML与JS混写；
+ 同样采用虚拟DOM（不总是直接操作dom），Diff算法（最小化页面重绘）高效。

#### 官网

英文官网:[ https://reactjs.org/](https://reactjs.org/)

中文官网: https://react.docschina.org/

### React的基本使用

1. #### 快速上手React 

   - html中准备一个React容器,用作react的作用范围

   - ```html
     .....
     <div id="box"></div>
     <!--你可以像这样在 <body> 标签内的任意位置放置一个“容器” <div>。根据需要，你可以在一个页面上放置多个独立的 DOM 容器。它们通常是空标签 —— React 会替换 DOM 容器内的任何已有内容。-->
     .....
     ```

   - 添加Script标签

   - ```js
     #在 </body> 结束标签之前，向 HTML 页面中添加以下标签：
     <script crossorigin src="https://unpkg.com/react@16/umd/react.development.js"></script>
     <script crossorigin src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
     <script>
     	#在此书写你的React代码
       // 创建虚拟dom
       let vdom = React.createElement('span', {
         className: 'demo'
       }, 'wanglogn');
       let Vdom1 = React.createElement('h1', {
         id: "first"
       }, 'React_createElement_h1',vdom);
       // 渲染虚拟dom到页面真实dom中
       let box = document.getElementById('box');
       ReactDOM.render(Vdom1, box);
     
     </script>
     
     #语法解释
     1.React 提供了createElement(type,props,[...child])方法返回指定类型的新 React 元素(虚拟dom)，
     type：dom类型
     props:虚拟dom的属性
     child:子元素
     2.ReactDOM提供 render(virtualDOM, containerDOM) 将虚拟DOM元素渲染到页面中的真实容器DOM中显示
     virtualDOM:js或jsx创建的虚拟dom对象
     containerDOM:用来包含虚拟DOM元素的真实dom元素对象(div)
     
     ###劣势
     1.以上创建虚拟dom的方式繁琐冗余，不能很方便的大量创建虚拟dom ----  解决方案  jsx语法
     2.script便签引入形式难以实现单页面应用，对前端工程化不友好   ----  解决方案  React脚手架创建应用
     ```

   

2. #### 创建React应用

   Create React App

   ### 先通过npm i -g create-react-app下载脚手架 创建项目create-react-app xxx
   
   ![image-20221017163552032](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20221017163552032.png)
   
   ```
   npx create-react-app name   || npm init react-app my-app
   cd name
   npm start
   ```

   ![createapp](assets/createapp.png)
   
   - reportWebVitals：性能分析文件
   
     - web-vitals是Google发起的，旨在提供各种质量信号的统一指南，我们相信这些质量信号对提供出色的网络用户体验至关重要。
       其可获取三个关键指标（CLS、FID、LCP）和两个辅助指标（FCP、TTFB）

     - FCP:首次内容绘制是浏览器将第一个DOM渲染到屏幕的时间，可以是任何文本、图像、SVG等的时间

       TTFB:指浏览器发起第一个请求到数据返回第一个字节所消耗的时间，这个时间包括了网络请求时间、后端处理时间

       LCP:代表在viewport中最大的页面元素加载时间

       CLS:是衡量用户[视觉稳定性的](https://web.dev/user-centric-performance-metrics/#types-of-metrics)一项重要的以用户为中心的度量标准

   - App.test.js: 测试用例文件   npm test

     
   
   2. 在项目中导入两个相关的包：
   
   ```
   // 1. 在 React 学习中，需要安装 两个包 react  react-dom
   // 1.1 react 这个包，是专门用来创建React组件、组件生命周期等这些东西的；
   // 1.2 react-dom 里面主要封装了和 DOM 操作相关的包，比如，要把 组件渲染到页面上
   import React from 'react'
   import ReactDOM from 'react-dom'
   ```
   
   3. 使用JS的创建虚拟DOM节点：
   
   ```
   // 2. 在 react 中，如要要创建 DOM 元素了，只能使用 React 提供的 JS API 来创建，不能【直接】像 Vue 中那样，手写 HTML 元素
   // React.createElement() 方法，用于创建 虚拟DOM 对象，它接收 3个及以上的参数
   // 参数1： 是个字符串类型的参数，表示要创建的元素类型
   // 参数2： 是一个属性对象，表示 创建的这个元素上，有哪些属性
   // 参数3： 从第三个参数的位置开始，后面可以放好多的虚拟DOM对象，这些参数，表示当前元素的子节点
   
   <h1>这是一个大大的H1</h1>
   var myH1 = React.createElement('h1', null, '这是一个大大的H1')
   
   // <div title="this is a div" id="mydiv" class="mydiv">这是一个div</div>
   var myDiv = React.createElement('div', { title: 'this is a div', id: 'mydiv' ,className:'mydiv'}, '这是一个div', myH1)
   ```
   
   4. 使用 ReactDOM 把元素渲染到页面指定的容器中：
   
   ```
   // ReactDOM.render('要渲染的虚拟DOM元素', '要渲染到页面上的哪个位置中')
   // 注意： ReactDOM.render() 方法的第二个参数，和vue不一样，不接受 "#app" 这样的字符串，而是需要传递一个 原生的 DOM 对象
   ReactDOM.render(myDiv, document.getElementById('app'))
   ```
   
   

### React与vue.js的对比

#### 虚拟Dom

- vue和react都采用了虚拟dom算法，以最小化更新真实DOM，从而减小不必要的性能损耗。

- Vue的虚拟dom是基于snabbdom库所做的修改，为了保证页面的最小优化，snabbdom引入了diff算法，通过Diff算法找出前后两个虚拟DOM之间的差异，只更新改变了的DOM节点，而不重新渲染为改变的DOM节点。

- react定义的一种类似于XML的JS扩展语法：JSX。作用是用来创建react虚拟DOM。React使用JSX编写虚拟DOM对象，经过Babel编译之后会生成真正的DOM. 然后会将真正的DOM插入(Render)到页面。

  

#### 组件化方面

1. 模块化：从 **代码** 的角度，去分析问题，把我们编程时候的业务逻辑，分割到不同的模块中来进行开发，这样能够**方便代码的重用**；
2. 组件化：从 **UI** 的角度，去分析问题，把一个页面，拆分为一些互不相干的小组件，随着我们项目的开发，我们手里的组件会越来越多，最后，我们如果要实现一个页面，可能直接把现有的组件拿过来进行拼接，就能快速得到一个完整的页面， 这样方**便了UI元素的重用**；**组件是元素的集合体**；
4. Vue是如何实现组件化的：.vue 组件模板文件，浏览器不识别这样的.vue文件，所以，在运行前，会把 .vue 预先编译成真正的组件；
 + template： UI结构
 + script： 业务逻辑和数据
 + style： UI的样式

4.React如何实现组件化：在React中实现组件化的时候，根本没有 像 .vue 这样的模板文件，而是，直接使用JS代码的形式，去创建任何你想要的组件；

 + React中的组件，都是直接在 js 文件中定义的（.js   /    .jsx）；
 + React的组件，并没有把一个组件 拆分为 三部分（结构、样式、业务逻辑），而是全部使用JS来实现一个组件的；（也就是说：结构、样式、业务逻辑是混合在JS里面一起编写出来的）

#### 移动APP开发
+ Vue，结合 Weex 这门技术，提供了 迁移到 移动端App开发的体验
+ React，结合 ReactNative，提供了迁移到 移动App的开发体验（RN用的最多，也是最火最流行的）；

#### 轻量化

都把注意力集中保持在核心库，而将其他功能如路由和全局状态管理交给相关的库。(vue-router、vuex、react-router、redux等等)



### React中几个核心的概念
#### 虚拟DOM（Virtual Document Object Model）
 + DOM的本质是什么：Document Object Model  页面元素  JS表示的UI界面元素 
 + DOM和虚拟DOM的区别：
   - DOM是由浏览器中的JS提供功能，所以我们只能人为的使用 浏览器提供的固定的API来操作DOM对象；
   - 虚拟DOM：并不是由浏览器提供的，而是我们程序员手动模拟实现的，类似于浏览器中的DOM，但是有着本质的区别；
 - 为什么要实现虚拟DOM：
    - JavaScript需要借助浏览器提供的DOM接口才能操作真实DOM，修改DOM经常导致页面重绘，所以一般来说，DOM操作越多，网页的性能就越差
    - 真实的DOM中，过多的内容修改，会带来多次的页面重绘，极大的损耗页面的性能。
    - 而在使用虚拟DOM时，不管一次修改了多少内容，最后只会发生一次页面的重绘，大大的提高了页面的性能。
    - 虚拟DOM设计的核心就是用高效的js操作，来减少低性能的DOM操作，以此来提升网页性能。
 - 虚拟DOM的目的： 
    - 虚拟DOM并不能消除原生的DOM操作，你仍然需要通过浏览器提供的DOM接口来操作真实DOM树，才能使页面发生改变。虚拟DOM的设计似乎是多此一举。
    - 但是虚拟DOM带来了一个重要的优势，那就是我们可以在完全不访问真实DOM的情况下，掌握DOM的结构
    - 如果我们本打算手动进行三次真实DOM操作，有了虚拟DOM结构后，把这三次DOM操作简化成了一次，这不就带来了性能上的提升![image-20210119062925366](assets/image-20210119062925366.png)
 - React中的虚拟dom
    - React中使用`jsx`语法定义模板时，React会用它生成一个由JavaScript描述的虚拟DOM树，并将其保存在JavaScript内存中。这个虚拟DOM树还保留了我们在模板中定义的数据和视图的绑定关系，这为React自动根据数据变化更新视图提供了可能。随后当数据发生变化时，React重新生成一个虚拟DOM树，通过对比两个虚拟DOM树的差异，React就可以知道该如何高效地更新视图。接着它就会调用原生的DOM接口，去更新真实DOM。



#### Diff算法

diff算法其实就是对DOM进行different比较的一种算法,简单来说Diff算法在虚拟DOM上实现，是虚拟DOM的加速器，提升性能的法宝.

React需要同时维护两棵虚拟DOM树：一棵表示当前的DOM结构，另一棵在React状态变更将要重新渲染时生成。React通过比较这两棵树的差异，决定是否需要修改DOM结构，以及如何修改。

 - tree diff:新旧DOM树，逐层对比的方式，就叫做 tree diff,每当我们从前到后，把所有层的节点对比完后，必然能够找到那些 需要被更新的元素；
 - component diff：在对比每一层的时候，组件之间的对比，叫做 component diff;当对比组件的时候，如果两个组件的类型相同，则暂时认为这个组件不需要被更新，如果组件的类型不 同，则立即将旧组件移除，新建一个组件，替换到被移除的位置；
 - element diff:在组件中，每个元素之间也要进行对比，那么，元素级别的对比，叫做 element diff；
 - key：key这个属性，可以把 页面上的 DOM节点 和 虚拟DOM中的对象，做一层关联关系；
![Diff算法图](assets/Diff.png)

### 作业：

1. 创建React应用

2. 预习jsx语法

   

### JSX语法&函数组件

### jsx语法

```js
#这种既不是字符串也不是 HTML的标签语法，我们称之为jsx
let vNode = <h1>Hello, world!</h1>;
```

JSX是一种JavaScript的语法扩展，运用于[React](https://baike.baidu.com/item/React/18077599)架构中，其格式比较像是模版语言，但事实上完全是在[JavaScript](https://baike.baidu.com/item/JavaScript/321142)内部实现的，它具有 JavaScript 的全部功能。元素是构成React应用的最小单位，JSX就是用来声明React当中的元素，React使用JSX来描述用户界面。

1. 当编译引擎，在编译JSX代码的时候，如果遇到了`<`那么就把它当作 HTML代码去编译，如果遇到了 `{}` 就把 花括号内部的代码当作 普通JS代码去编译；在{}内部，可以写任何符合JS规范的代码；

   ```js
   #如果要在 JSX 语法内部，书写 JS 代码了，那么，所有的JS代码，必须写到 {} 内部；
   let title = 'this is a title';
   let mydiv = <div> 
     这是使用功jsx语法创建的div元素
     <h1 title={title}>这是一个h1</h1> 
   </div>
   
   #在 JSX 语法中，你可以在大括号内放置任何有效的 JavaScript 表达式
   <li>{2 + 2}</li>
   <li>{fn()}</li>
   ```

   

2. JSX语法的本质：还是以 React.createElement 的形式来实现的，并没有直接把 用户写的 HTML代码，渲染到页面上，以下两种示例代码完全等效；

   ```js
   const element = (
     <h1 className="greeting">
       Hello, world!
     </h1>
   );
   
   const element = React.createElement(
     'h1',
     {className: 'greeting'},
     'Hello, world!'
   );
   ```

   

3. 因为 JSX[javascript xml] 语法上更接近 JavaScript 而不是 HTML，所以 React DOM 使用 `camelCase`（小驼峰命名）来定义属性的名称，而不使用 HTML 属性名称的命名约定。

   在JSX中，如果要为元素添加`class`属性了，那么，必须写成`className`，因为 `class`在ES6中是一个关键字；和`class`类似，label标签的 `for` 属性需要替换为 `htmlFor`.`tabindex` 则变为 tabIndex 。

   ```HTML
   <li className="lisi">李四</li>
   <label htmlFor="user">用户名</label>
   ```

4. 在JSX创建DOM的时候，所有的节点，必须有唯一的根元素进行包裹；

5. 如果要写注释了，注释必须放到 {} 内部

   ```
   {/* 我是注释 */}
   ```

### 函数组件

```
// 在react中，构造函数，就是一个最基本的组件
// 如果想要把组件放到页面中，可以把构造函数的名字，当做组件的名称，以html标签的形式引入页面中。
// 注意：react在解析所有的标签的时候，是以标签的首字母来区分的，
// 如果首字母是小写的，那么就是按照普通的html标签来解析的。
// 如果首字母是大写的，那么就按照组件的形式去解析。 
// 组件的首字母必须是大写
function Hello(){
 return <div>
  <h1>这是在Hello组件中定义的元素</h1>
 </div>
}
ReactDom.render(<Hello></Hello>,document.getElementById('root'));
```



父组件向子组件传递数据

```js
let obj = {
  name:'lisi',
  age:20,
  job:'xuesheng'
}
function Hello(props){
//在组件中，如果想要使用功外部传递过来 的数据，必须显示的在构造函数参数列表中，定义props属性来接收
//通过props得到的数据都是只读的，不能修改
// props.name = 'aaa';
  return <div>
    <h1>这是在Hello组件中定义的元素</h1>
    <div>姓名：{props.name}</div>
    <div>年龄：{props.age}</div>
    <div>工作：{props.job}</div>
  </div>
}
ReactDOM.render(
//展开运算符
  //<Hello {...obj}/>
    <Hello name={obj.name} age={obj.age} job={obj.job}>
  ,
  document.getElementById('root')
);
```



### 将组件封装到单独的文件中

src

​	components

​		hello.js 组件

```
hello.js组件

import React from 'react';
function Hello(props){
  return <div >
  <h1>这是在Hello组件中定义的元素</h1>
    <div>姓名：{props.name}</div>
    <div>年龄：{props.age}</div>
    <div>工作：{props.job}</div>
  </div>
}
export default Hello;
```

```
index.js
import Hello from './components/hello.js'
```

作业：

1. 以构造函数形式来定义组件，并实现组件之间传值

   ![image-20210120110600178](assets/image-20210120110600178.png)



## 第二章：class组件

### React中：第二种创建组件的方式

#### 基于class关键字创建组件
+ 使用 class 关键字来创建组件
```js
//使用class创建的类，通过extents关键字，继承了React.Component之后，就是一个组件的模板了。
class Person extends React.Component{
    render(){
        // 在render函数中，必须返回一个null或者符合规范的虚拟DOM元素
        return <div>
            <h1>这是用 class 关键字创建的组件！</h1>
        </div>;
    }
}

```

#### class组件传值

```js
//在function创建的组件中，如果想使用props,就必须先定义，否则无法使用，
//但是在class中定义的组件中，可以直接用this.props来直接访问。不需要预先接收props
//注意：无论在function中还是在class中，props都是只读的

class Hello extends React.Component {
  constructor(props){
    // 在使用extends实现的继承，要在constructor第一行，一定要显示的调用super()
    // spuer表示父类的构造函数，是父类constructor的引用
    super(props);
    // 在constructor中，如果想要访问props属性，不能直接使用this.props
    // 而是要在constructor的构造函数参数列表中，显示的定义props参数来接收，才能正常使用props
    // 在super()中添加props后，可以直接使用this.props，否则的话只能直接使用参数props
    
    console.log(this.props.name);
  }
  render() {
    console.log(this);
    // this.props.name = 'ergou';
    return <div>
        sdfsdf{this.props.name}
    </div>

  }
}
```

#### 组件中的私有属性state

```js
在组件中，我们可以定义state来实现私有属性，除了拥有并设置了它的组件，其他组件都无法访问。
State 与 props 类似，但是 state 是私有的，并且完全受控于当前组件。
constructor(){
    this.state = {
    	comment:'这是个私有属性'
    }
}
注意：
1.不要直接修改 State
// Wrong
this.state.comment = 'Hello';
而是应该使用 setState():
// right
this.setState({comment: 'Hello'});

1.1
<button onClick={this.changestate}>修改数据</button>
//事件处理函数要写成箭头函数
changestate=()=>{
    this.setState({
      msg: 'msg'
    });
  }
//如果是普通函数，this指向丢失，指向的是undefined
changestate(){
    console.log(this); // undefined
}
//原因,这不是React的原因，这是JavaScript中本来就有的。如果你传递一个函数名给一个变量，然后通过在变量后加括号()来调用这个方法，此时方法内部的this的指向就会丢失。
let obj = {
  name: 'lisi',
  say() {
    console.log(this.name)
  },
}
obj.say();//lisi

let d = obj.say
d()//error
//解决办法：在调用的时候使用bind绑定this


1.2 数据双向绑定
  <input type="text" value={this.state.msg} onChange={this.iptchange}/>
  iptchange=(event)=>{
    /*event.persist();*/
    console.log(event.target.value);
    this.setState({
      msg: event.target.value
    });
    console.log(this.state);//可以看出this.setState是一个异步的过程
  }


2.State 的更新可能是异步的
出于性能考虑，React 可能会把多个 setState() 调用合并成一个调用。
因为 this.props 和 this.state 可能会异步更新，所以你不要依赖他们的值（state）来更新下一个状态。

setState方法，也支持传递一个function 作为参数，并且要在function内部，必须return一个对象。
在function的参数中，支持传递两个参数，其中，第一个是state(数据修改之前的老的state数据)
第二个参数，是外界传入组件的数据props
iptchange=()=>{
    this.setState(function(oldstate,props){
      console.log(ostate);
      return {
        info:'is changed'
      }
    });
  }s
  
或者以下方式：
   this.setState(function(ostate,props){
      // console.log(ostate);
      return {
        msg: '我是修改过后的msg'
      }
    },function(){
      // 在第二个回调函数中来，获取你修改过之后的数据
      console.log(this.state);
      // 利用这个修改后的数据。做后序的功能
    });


3.单向数据流，组件可以选择把它的 state 作为 props 向下传递到它的子组件中
这通常会被叫做“自上而下”或是“单向”的数据流。任何的 state 总是所属于特定的组件，而且从该 state 派生的任何数据或 UI 只能影响树中“低于”它们的组件。

如果你把一个以组件构成的树想象成一个 props 的数据瀑布的话，那么每一个组件的 state 就像是在任意一点上给瀑布增加额外的水源，但是它只能向下流动。


```



### 两种创建组件方式的对比

//注意:以上两种创建组件的方式，有着本质上的区别，其中，
/使用function构造函数创建的组件，内部没有state私有数据，只有一个props来接收外界传递过来的数据;
//使用class关键字创建的组件，内部，除了有this.props这个只读属性之外，还有一个专门用于存放自己私有
数据的this.state属性，这个state是可读可写的!
/基于上面的区别:我们可以为这两种创建组件的方式下定义了:

使用function创建的组件，叫做【无状态组件】﹔

使用class创建的组件，叫做【有状态组件】
//有状态组件和无状态组件，最本质的区别，就是有无state属性;

同时，class创建的组件，有自己的生命周期函数，
但是，function创建的组件，没有自己的生命周期函数;

//问题来了:什么时候使用有状态组件，什么时候使用无状态组件呢???
//1.如果一个组件需要存放自己的私有数据，或者需要在组件的不同阶段执行不同的业务逻辑，此时，非常适合用class
创建出来的有状态组件;
1/2.如果一个组件，只需要根据外界传递过来的props，渲染固定的页面结构就完事儿了，此时，非常适合使用
function创建出来的无状态组件;(使用无状态组件的小小好处:由于剔除了组件的生命周期，所以，运行速度会相对快一些

### 作业：

1. ![image-20210121112402977](assets/image-20210121112402977.png)

React中引入图片的方式

```
#  demo.jsx 组件
#引入
import img1 from './../assets/image/xxx.jpeg';
或
const img2 = require('./../assets/image/xxx.jpeg');

#使用
<img src={img1}>
<div style={{background:`url(${img2}) center center no-repeat`}}>
或
<img src={require('./../assets/image/xxx.jpeg')}>

```



### React-style

### 一个小案例，巩固有状态组件和无状态组件的使用
#### 通过for循环生成多个组件

1. 数据：
```
CommentList = [
    { user: '张三', content: '哈哈，沙发' },
    { user: '张三2', content: '哈哈，板凳' },
    { user: '张三3', content: '哈哈，凉席' },
    { user: '张三4', content: '哈哈，砖头' },
    { user: '张三5', content: '哈哈，楼下山炮' }
]
1.数组渲染
2.jsx语法
3.抽离组件
```

### style样式

1. 可以外部引入css文件

```
1. 有样式覆盖情况
style.css     
引入 import './style.css'    

2.避免组件样式覆盖
可以分模块定义   style.module.css
import style from './style.module.css'

3.sass 
npm install node-sass  
 style.module.scss
```

 2.使用普通的style样式，style 中不能直接写样式，此时不是真正的html 而是jsx语法，所写的都是一些js语句，所以在次数，style = {{}}  外层{} 是jsx语法书写js代码的形式， 内层{}是一个对象来表现样式

样式优化1 样式提出来，作为js变量 

const userStyle = {fontSize: '14px'};

样式优化2 如果有很多样式，可以统一保存在一个样式对象中

```
const styles = {
    item: {border: '1px dashed #ccc', margin: '10px', padding: '10px', boxShadow: '0 0 #ccc'},
    user: {fontSize: '14px'},
    content: {fontSize: '12px'}
}
```

样式优化3 把样式封装到js文件中。

```
style.js
export default{
    item: {border: '1px dashed #ccc', margin: '10px', padding: '10px', boxShadow: '0 0 10px #ccc'},
    user: {fontSize: '14px'},
    content: {fontSize: '12px'}
}

import styles from '@/components/styles.js'
```



推荐文章：

https://zhuanlan.zhihu.com/p/110533397

https://www.jianshu.com/p/8ba5fe0c4215





## 第三章：React生命周期

### 组件的生命周期

 + 概念：在组件创建、到加载到页面上运行、以及组件被销毁的过程中，总是伴随着各种各样的事件，这些在组件特定时期，触发的事件，统称为 组件的生命周期；

 + 注意：在React版本更新过程中，有些钩子函数被遗弃了（官方手册有提示）。

 + 组件生命周期分为三部分：

 + ![image-20211018205423623](assets/image-20211018205423623.png)

   ![React生命周期图](assets/React%E7%94%9F%E5%91%BD%E5%91%A8%E6%9C%9F%E5%9B%BE.png)
   
   - **组件挂载阶段**：组件创建阶段的生命周期函数，有一个显著的特点：创建阶段的生命周期函数，在组件的一辈子中，只执行一次；
   
     - constructor:如果不初始化 state 或不进行方法绑定，则不需要为 React 组件实现构造函数
     - render：第一次开始渲染真正的虚拟DOM，当render执行完，内存中就有了完整的虚拟DOM了，但是页面尚未显示dom元素
       - 在return之前虚拟dom还没有开始创建，页面上拿不到任何元素 
       - return执行完毕后，虚拟dom创建好了，但是还没有挂在到页面上。
     - componentDidMount: 组件完成了挂载，此时，组件已经显示到了页面上，当这个方法执行完，组件就进入都了 运行中 的状态，页面，虚拟内存中，数据保持一致。 
       -  最早只能在此函数中操作dom元素
       - 相当于vue中的mounted钩子函数
       - 此组件执行完，就进入到了运行中的状态，所以此函数是组件创建阶段的最后一个函数
   
   - **组件运行阶段**：也有一个显著的特点，根据组件的state和props的改变，有选择性的触发0次或多次；
   
     - shouldComponentUpdate(nextProps, nextState): 组件是否需要被更新，此时，组件尚未被更新，但是，state 和 props 肯定是最新的
   
       - 此函数中要求必须返回一个boolean 如果返回一个fasle,则不会继续执行后续的生命周期函数，而是直接退回到了运行中状态，此时后续的render函数并没有被执行，因此页面不会被更新，但是组件中的state状态，却被修改了
   
       - 可以通过不同的条件来指定后续的执行效果
   
         - 偶数次累加
   
         - ```
           // console.log(this.state.num);
           // return nextState.num %2 ===0?true:false;
           ```
   
     - render: 此时，又要重新根据最新的 state 和 props 重新渲染一棵内存中的 虚拟DOM树，当 render 调用完毕，内存中的旧DOM树，已经被新DOM树替换了！此时页面还是旧的
   
     - componentDidUpdate(prevProps, prevState): 此时，页面又被重新渲染了，state 和 虚拟DOM 和 页面已经完全保持同步
   
       -  组件完成了更新，此时，state中的数据、虚拟DOM、页面上的DOM，都是最新的，此时，你可以放心大胆的去操作页面了
   
   - **组件销毁阶段**：也有一个显著的特点，一辈子只执行一次；
   
     - componentWillUnmount: 组件将要被卸载，此时组件还可以正常使用；

### defaultProps

> 在组件创建之前，会先初始化默认的props属性，这是全局调用一次，严格地来说，这不是组件的生命周期的一部分。在组件被创建并加载候，首先调用 constructor 构造器中的 this.state = {}，来初始化组件的状态。
>
> 1. 给组件设置默认props属性：
>
>    ```
>    static defaultProps = {
>    	num:100
>    }
>    ```
>
> 2. 给属性进行类型校验，需要先运行`cnpm i prop-types --save`
>
> 3. import  Types from 'prop-types'
>
> 4. static propTypes  = {number:Types .number}

### 了解生命周期函数

React生命周期的回调函数总结成表格如下：
![image-20221022105005252](C:\Users\Lenovo\AppData\Roaming\Typora\typora-user-images\image-20221022105005252.png)
被新版本摒弃的钩子函数

+ Mounting：

 - componentWillMount() （新版本已摒弃）
   -  组件即将挂在到页面上时执行，此时还没有挂在到页面上 ，虚拟dom也没开始创建
   -  等同于vue中的created钩子函数
   -  无法获取dom
   -  能获取到props
   -  能获取到state
   -  能调用自定义函数

+ Updating：

 - componentWillReceiveProps(nextProps) （新版本已摒弃）

   - 组件将要接收外界传递过来的新的props属性值
   - 当子组件第一次被渲染到页面上的时候，不会触发这个函数
   - 只有当父组件中，通过某些事件，重新修改了传递给子组件的props 数据之后，才会触发
   - 获取的数据不是最新，
   - 最新的数据通过参数来获取

 - componentWillUpdate(nextProps, nextState) （新版本已摒弃）

   - 组件将要更新，此时尚未更新，在进入这个生命周期函数的时候，内存中的虚拟DOM是旧的，页面上的DOM元素也是旧的

   - 此时页面上的 DOM节点，都是旧的，应该慎重操作，因为你可能操作的是旧DOM     看：innerhtml

     ```
     获取dom元素
     1.原生方式
     2.ref属性
     ```


### React组件练习

### 绑定this并传参的三种方式

1. 在事件中绑定this并传参：

```
{/* bind的作用：为前面的函数，修改函数内部的this指向，让函数内部的this，指向bind参数列表中的第一个参数 */}
{/* bind和call、apply */}
{/*call、apply修改完this指向后，会立即调用前面的函数，但是bind只能修改this指向，并不会调用  */}
{/* bind中第一参数用来修改this指向，第一个后面的参数，都会是前面函数的参数 */}
    <input type="button" value="在事件中绑定this并传参" onClick={this.handleMsg1.bind(this, 'a', 'b')} />

    // 在事件中绑定this并传参
    handleMsg1(arg1, arg2) {
        console.log(this);
        // 此时this是个null
        this.setState({
            msg: '在事件中绑定this并传参：' + arg1 + arg2
        });
    }
    
    
```

2. 在构造函数中绑定this并传参:

```
    // 修改构造函数中的代码：
    this.handleMsg2 = this.handleMsg2.bind(this, 'a', 'b');

    <input type="button" value="在构造函数中绑定this并传参" onClick={this.handleMsg2} />

    // 在构造函数中绑定this并传参
    handleMsg2(arg1, arg2) {
        this.setState({
            msg: '在构造函数中绑定this并传参：' + arg1 + arg2
        });
    }
```

3. 用箭头函数绑定this并传参：

```
    <input type="button" value="用箭头函数绑定this并传参" onClick={() => { this.handleMsg3('a', 'b') }} />

    // 用箭头函数绑定this并传参
        handleMsg3(arg1, arg2) {
            this.setState({
                msg: '用箭头函数绑定this并传参：' + arg1 + arg2
            });
        }
        
        
注意：
<input type="button" value="用箭头函数绑定this并传参" onClick={this.handleMsg3('a', 'b') }/>
！！！onClick={如果传参（加括号）。此中函数，会自动调用}

 handleMsg3=(arg1, arg2)=>{
            this.setState({
                msg: '用箭头函数绑定this并传参：' + arg1 + arg2
            });
        }


```

### 子组件向父组件传递数据

- React中，数据是从上向下流动的，也就是一个父组件可以把它的 state/props通过props传递给它的子组件，但是子组件，不能修改props，如果组件需要修改父组件中的数据，则可以通过回调的方法来完成，

- 说白了就是子组件想要修改父组件的值，就是在父组件调用子组件的地方，传递一个方法，该方法首先在父组件中定义，子组件通过props的获取到父组件传递的方法，子组件就可以调用该方法

- ```
  子组件==》父组件传递数据
  vue： 
  子组件中【 抛出事件监听 $emit(事件名，参数)  】
  父组件中【监听事件    @事件名='父组件中的事件处理函数'   】
  
  react：
  子组件中：【在事件中，使用 this.props.自定义事件名（参数/传递的数据）】
  父组件中：【父组件调用子组件的地方，添加一个事件监听，来监听子组件中挂载在props属性中的事件】
  
  父组件调用子组件
  <Cmtbox senddata={this.send}></Cmtbox>
  send=(e)=>{
      console.log(e);
      this.state.list.unshift(e);
      this.setState({
        list:this.state.list
      });
    }
    
  子组件
  <input type="button" value="发表评论" onClick={this.send}/>
  send(){
      let obj = {
        user: this.use.current.value,
        content: this.cont.current.value
      }
      this.props.senddata(obj);
    }
  ```

  

## 第四章：ReactRouter

https://v5.reactrouter.com/

1.react-router

 安装：

```js
npm install react-router-dom@5
```

导入：

```
import {
	HashRouter, 
	BrowserRouter as Router,
	//表示一个路由根容器，所有的路由相关的东西，都要包裹在HashRouter（BrowserRouter）里面，
	//而且，一个网站中，只需要使用一次HashRouter（BrowserRouter）,在HashRouter（BrowserRouter）中，只能有一个根元素
	//BrowserRouter  h5 history 模式 
	//HashRouter   hash模式
  
  Route,  
  //Route表示一个路由规则，在Route上，有两个比较重要的属性，path,component  除了是规则 还是占位符
  //类似于vue中的<router-view></router-view>
  
  Link 
  //表示一个路由的链接，类似于vue中的<router-link to=""></router-link>
}
```

```
import React, { Component } from 'react';
import {
  BrowserRouter as Router,
  Switch,
  HashRouter,
  Route,
  Link
} from "react-router-dom";


import Home from './component/home.jsx'
import mine from './component/mine.jsx'
import news from './component/set.jsx'
class App extends Component {
  render() {
    return <div>
      <HashRouter>
        <Link to='/home'>首页</Link>
        <Link to='/mine'>我的</Link>
        {/* 路由传参 */}
        <Link to='/news/hot/01'>新闻</Link>
      <div>
          <Switch>
          <Route path='/home' component={Home}></Route>
          <Route path="/mine" component={mine}/>
            {/* 路由传参  exact 精确匹配   在组件中使用props来接收参数 props.match.params  */}
          <Route path="/news/:type/:id" exact component={news}/>
          <Route path="/news" exact component={news}/>
          </Switch>
      </div>
      </HashRouter>
    </div>
  }
}

export default App;
```

### 重定向

```
//根目录重定向到首页
<Route path="/">
	<Redirect to="/home"></Redirect>
	<Redirect to={{ pathname: '/home', search: 'a=aaa',}}></Redirect>
</Route>

```

![image-20210517222031540](assets/image-20210517222031540.png)

### NavLink

NavLink:一个特殊版本的Link 可以添加激活状态的类名 或者样式

```
<NavLink to="/home" activeClassName="active_aaa">首页</NavLink>
activeClassName 激活状态的类名  默认是active   可以自行修改
```

### Switch

  //有<Switch>标签，则其中的<Route>在路径相同的情况下，只匹配第一个，这个可以避免重复匹配；

```
<Switch>
	//相同路径只会匹配一个
    <Route path="/home" component={Home}></Route>
    <Route path="/home" component={Home}></Route>
    <Route path="/list" component={List}></Route>
    <Route path="/about" component={About}></Route>
</Switch>
```

  //无<Switch>标签，则其中的<Route>在路径相同的情况下全都会匹配。更严重的是，还会匹配上级路径的

```
// 此时 Home组价会一直存在， /list /home /about 的上级路径是/
<Route path="/" component={Home}></Route>
<Route path="/home" component={Home}></Route>
<Route path="/list" component={List}></Route>
<Route path="/about" component={About}></Route>
```



### 二级路由：

```
import React, { Component } from 'react';
import { BrowserRouter as Router, Link, Route ,Switch } from 'react-router-dom'
import Details from './details'
class set extends Component {
  render() {
    return (
      <div>
        新闻组件
        <Router>
          <ul>
            <li><Link to="/news/details/01">新闻一</Link></li>
            <li><Link to="/news/details/02">新闻二</Link></li>
            <li><Link to="/news/details/03">新闻三</Link></li>
            <li><Link to="/news/details/04">新闻四</Link></li>
          </ul>
          <hr/>

          <Switch>
          	//传参数给新闻详情组件，引出组件传值
            <Route path="/news/details/:id" component={Details}/>
          </Switch>

        </Router>
      </div>
    );
  }
}

export default set;
```



### 路由传参:

```
params:
<Route path='/path/:name' component={Path}/>
声明式：<link to="/path/2">xxx</Link>
编程式：this.props.history.push({pathname:"/path/" + name});
//读取参数用:this.props.match.params.name
```

```
query:
<Route path='/query' component={Query}/>
<Link to={{ pathname : ' /query' , query : { name : 'sunny' }}}>
this.props.history.push({pathname:"/query",query: { name : 'sunny' }});
//读取参数用: this.props.location.query.name
```

```
state:
<Route path='/sort ' component={Sort}/>
<Link to={{ path : ' /sort ' , state : { name : 'sunny' }}}> 
this.props.history.push({pathname:"/sort ",state : { name : 'sunny' }});
//读取参数用: this.props.location.state.name
```

```
search:
<Route path='/web/departManange ' component={DepartManange}/>
<link to="web/departManange?tenantId=12121212">xxx</Link>
this.props.history.push({pathname:"/web/departManange?tenantId" + row.tenantId});
//读取参数用: this.props.location.search
```



### AntDesign: 参阅手册

## 第五章：React案例

需求：

- create-react-app脚手架搭建项目
- 项目基本布局实现
- antDesign UI组件库
- 使用reactRouter实现一级路由、二级路由、路由传参
- fetch API 实现数据加载

![](assets/4.png)

![](assets/2.png)

![](assets/1.png)

![](assets/3.png)

```js
APP.js
import React, { Component } from 'react'
import { Layout, Menu } from 'antd'
import './App.css'
const { Header, Content, Footer } = Layout
class App extends Component {
  render() {
    return (
      <Layout className="layout">
        <Header>
          <div className="logo" />
          <Menu theme="dark" mode="horizontal" defaultSelectedKeys={['2']}>
            <Menu.Item>首页</Menu.Item>
            <Menu.Item>电影</Menu.Item>
            <Menu.Item>关于</Menu.Item>
          </Menu>
        </Header>
        <Content style={{ padding: '0 50px' }}>
          <div className="site-layout-content">Content</div>
        </Content>
        <Footer style={{ textAlign: 'center' }}>
          Ant Design ©2018 Created by Ant UED
        </Footer>
      </Layout>
    )
  }
}

export default App

```

```js
movie.jsx
import React, { Component } from 'react'
import { Route, Link, Redirect, Switch } from 'react-router-dom'
import List from './list'
import { Layout, Menu } from 'antd'
const { Sider, Content } = Layout

class home extends Component {
  render() {
    return (
      <Layout style={{ height: '100%' }}>
        <Sider style={{ background: '#fff' }}>
          <Menu
            style={{ width: 200 }}
            defaultSelectedKeys={['theaters']}
            mode="inline"
          >
            <Menu.Item key="theaters">
              <Link to="/movie/list/in_theaters">正在热映</Link>
            </Menu.Item>
            <Menu.Item key="soon">
              <Link to="/movie/list/coming_soon">即将上映</Link>
            </Menu.Item>
            <Menu.Item key="top250">
              <Link to="/movie/list/top250">Top250</Link>
            </Menu.Item>
          </Menu>
        </Sider>
        <Content>
          <Switch>
            <Route path="/movie" exact>
              <Redirect to="/movie/list/in_theaters"></Redirect>
            </Route>
            <Route path="/movie/list/:type" component={List}></Route>
          </Switch>
        </Content>
      </Layout>
    )
  }
}

export default home

```

```js
list.jsx
import React, { Component } from 'react'

class list extends Component {
  constructor(props) {
    super(props)
    this.state = {
      list: [],
      type: '',
    }
    this.init_data = this.init_data.bind(this)
  }

  init_data(t) {
    // 请求
    fetch(`http://localhost:10010/movie/${t}`)
      .then((res) => {
        return res.json()
      })
      .then((res) => {
        console.log(res)
        this.setState({
          list: res.subjects,
        })
      })
  }

  componentDidMount() {
    console.log(0)
    this.init_data(this.props.match.params.type)
  }

  // componentDidUpdate() {
  // console.log('111')
  // this.init_data(this.props.match.params.type)
  // }

  componentWillReceiveProps(props_) {
    this.init_data(props_.match.params.type)
  }

  render() {
    return (
      <div>
        {this.state.list.map((item) => {
          return <h1>{item.title}</h1>
        })}
      </div>
    )
  }
}

export default list

```

