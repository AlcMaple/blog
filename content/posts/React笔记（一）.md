+++

author = "Maple"
title = "React笔记（一）"
date = "2024-07-19"
description = "这是一个React学习笔记，持续更新"
tags = [
    "markdown",
    "React",
    "JavaScript",
    "CSS",
    "HTML",
]
categories = [
    "Web前端",
    "React",
]
series = ["Web前端"]
aliases = ["React1"]

+++

本文提供了React的基础语法和基本知识点，帮助人们快速理解和上手React

<!--more-->

# `React`介绍

## 知识程度

- 了解：
- 熟悉：
- 掌握：
- 精通：

## `React`是什么

`React`是一个用于**构建Web和原生交互界面的库**

- 用途
  - 网页加载速度更快

## `React`的优势

组件化的开发方式

性能更高

跨平台支持

# 开发环境搭建

## 使用`create-react-app`快速搭建开发环境（脚手架方式创建`React`项目）

使用`vscode`编译器，自主选择一个目录

打开终端

执行命令：`npx create-react-app react-basic`

> `npx`：`Node.js`工具命令，用于查找并执行后续的包命令
>
> `create-react-app`：核心包(固定写法)，用于创建`React`项目
>
> `react-basic`：`React`项目的名称，可以自定义

`cd react-basic`进入项目

`npm start`启动项目

# `JSX`基础-概念和本质

## 什么是`JSX`

概念：`JSX`是`Javascript`和`XML(HTML)`的缩写，表示在**`JS`代码中编写`HTML`模板结构**，它是`React`中编写`UI`模板的方式

这是最基本的框架，必须要有，缺一不可

```react
function App() {
  return (
    <div>
      
    </div>
  );
}

export default App;
```

## `JSX`的本质

`JSX`不是标准的`JS`语法，是**`JS`的语法扩展**，浏览器本身不能识别，需要通过**解析工具做解析**才能在浏览器中运行

# `JSX`基础-高频场景

## `JSX`中使用`JS`表达式

在`JSX`中，通过**大括号语法{}**识别`Javascript`中的表达式

## `JSX`中实现复杂条件渲染

- 需求：列表中需要根据文章状态适配三种情况，单图，三图和无图三种模式
- 解决方案：**自定义函数+`if`判断语句**

```react
function messType(num) {
  if (num == 1) {
    return '单图模式'
  }
  else if (num == 3) {
    return '三图模式'
  }
  else {
    return '无图模式'
  }
}

let number = 0

function App() {
  return (
    <div>
      <h1>{messType(number)}</h1>
      <h1>{messType(number + 1)}</h1>
      <h1>{messType(number + 3)}</h1>
    </div>
  );
}

export default App;
```

# `React`中的事件绑定

## `React`基础事件绑定

- 语法：`on + 事件名称 = {事件处理程序}`

```react
function App() {
  function clickHandle() {
    console.log('button被点击了');
  }
  return (
    <div>
      <button onClick={clickHandle}>点击我</button>
      {/* <button onClick={function () {
        console.log('button被2点击了')
      }}>点击我</button> */}
    </div>
  );
}

export default App;
```

## 使用事件对象参数

- 语法：在事件回调函数中**设置形参e**

```react
function App() {
  function clickHandle(e) {
    console.log('button被点击了', e);
  }
  return (
    <div>
      <button onClick={clickHandle}>点击我</button>
    </div>
  );
}

export default App;
```

## 传递自定义参数

- 语法：事件绑定位置改造**成箭头函数**

不能直接写函数调用，需要一个**函数引用**

```react
function App() {
  function clickHandle(name) {
    console.log('button被点击了', name);
  }
  return (
    <div>
      <button onClick={() => clickHandle('jack')}>点击我</button>
    </div>
  );
}

export default App;
```

若不改造成箭头函数，会变成自动调用2次，并且点击事件无效

## 同时传递事件对象和自定义参数

```react
function App() {
  function clickHandle(e, name) {
    console.log('button被点击了', name, e);
  }
  return (
    <div>
      <button onClick={(e) => clickHandle(e, 'jack')}>点击我</button>
    </div>
  );
}

export default App;
```

# `React`中的组件

## `React`组件

组件：**首字母大写的函数**，内部存放组件的逻辑和视图`UI`，渲染组件时，把组件**当成标签书写**即可

```react
// 定义组件
function Button() {
  return <button>clike me</button>
}

function App() {
  return (
    <div>
      {/* 组件的两种使用方式 */}
      <Button />
      <Button></Button>
    </div>
  );
}

export default App;
```

# `useState`

## `useState`基础使用

`useState`是一个函数，通过向组件添加**状态变量**来控制组件的渲染结果

- 本质：状态变量发生变化，组件的视图`UI`也跟着变化**(数据驱动视图)**，即达到实时更新的效果
- 应用：评论发布，评论列表实时更新

```react
const [count, setCount] = useState(0);
```

1. `useState`返回值是数组
2. 数组中，第一个参数是状态变量，第二个参数是`set`函数，用来修改状态变量
3. `useState`的参数作为`count`的初始值

# 修改状态的规则

## 状态不可变

在`React`中，状态被认为是只读，直接修改状态不能引发视图更新，通过`set`函数进行修改才能引发视图更新

```react
// 导入useState钩子
import { useState } from 'react';

function App() {
  const [count, setCount] = useState(0);
  const handleClick = () => {
    // 直接修改，无法引发视图更新
    // count++
    // console.log(count);

    // 用set函数传入新值来修改count，会自动重新使用新的count来渲染UI
    setCount(count + 1);
    console.log(count);
  }
  return (
    <div>
      <button onClick={handleClick}>增加</button>
    </div>
  );
}

export default App;
```

- 注意
  - 使用`useState`钩子，需要导入
  - useState是异步更新的，因此上述代码在每次点击时，控制台输出的是点击前的结果，想立即获取到更新的值可以通过useEffect实现

运行机制：点击按钮，调用`handleClick`函数，当调用`setCount`函数时，`React`将新的`state`**放入队列中**，继续执行后面的代码`console.log(count)`，然后开始**渲染**，将`count`赋值为`count+1`

## 修改对象状态

- 规则：`set`一个**全新的对象**来进行修改

```react
// 导入useState钩子
import { useState } from 'react';

function App() {
  const [form, setForm] = useState({
    name: 'jack'
  });
  const handleClick = () => {
    setForm({
      name: 'john'
    })
    console.log(form.name);
  }
  return (
    <div>
      <button onClick={handleClick}>点击我</button>
    </div>
  );
}

export default App;
```

# 组件的样式处理

## 组件基础样式方案

```css
.color{
  color: red;
}
```

```react
import './index.css'
function App() {
  return (
    <div>
      {/* 行内样式 */}
      <p class='color'>我是p标签</p>
      {/* class类名控制 */}
      <span style={{ color: 'green' }}>我是span标签</span>
    </div>
  );
}

export default App;
```

`css`中使用的是`.`，因此在`UI`设计中，也要用`class`或者`className`作为属性，否则样式不生效

# 案例：B站评论

## B站评论案例

![B站评论案例效果图](/images/react/b站评论案例效果图.png)

- 需求
  - 渲染评论列表
  - 删除评论实现
  - 渲染导航`Tab`和高亮实现
  - 评论列表排序功能实现

## 渲染评论列表

- 核心思路
  - 使用`useState`维护评论列表
  - 使用**`map`方法**对列表数据进行遍历渲染

```react
// 导入useState钩子
import { useState } from 'react';

// 评论列表数据
const list = [
  '评论1', '评论2', '评论3'
]

function App() {
  // 使用useState维护评论列表
  const [comments, setComments] = useState(list);
  // 定义一个函数，用于添加评论到列表
  function addComment() {
    let comment = document.querySelector('input').value;
    // ...comments:获取列表当前的所有数据，并返回一个列表
    // 更新comments状态，将comment添加到comments列表的末尾，并且React会重新渲染列表
    setComments([...comments, comment]);
    document.querySelector('input').value = '';
  }
  return (
    <div>
      <div>
        <input type="text" placeholder='发一条友善的评论'></input>
        <button onClick={addComment}>发布</button>
      </div>

      {/* 评论列表 */}
      <div>
        <ul>
        {/* 使用map方法对列表数据进行遍历渲染 */}
          {comments.map(item => (
            <li>{item}</li>
          ))}
        </ul>
      </div>
    </div>
  );
}

export default App;
```

## 实现评论删除

- 需求：
  - 只有自己的评论才显示删除按钮
  - 点击删除按钮，删除当前评论，列表中不再显示
- 核心思路
  - 删除显示 - 条件渲染
  - 删除功能 - 拿到当前项`id`，以`id`为条件对评论列表做`filter`过滤

```react
// 导入useState钩子
import { useState } from 'react';

// 评论列表数据
const list = [{
  uid: 1,
  content: '评论1'
},
{
  uid: 2,
  content: '评论2'
},
{
  uid: 3,
  content: '评论5'
}]

// 当前登录账号的uid
const uid = 123;

function App() {
  // 使用useState维护评论列表
  const [comments, setComments] = useState(list);
  // 定义一个函数，用于添加评论到列表
  function addComment() {
    let comment = document.querySelector('input').value;
    let id = uid
    let tempObject = {
      uid: id,
      content: comment
    }
    setComments([...comments, tempObject]);
    document.querySelector('input').value = '';
  }

  function handleDel(id,index) {
    // filter方法：满足条件保留
    let tempList = comments.filter((item,i) => i!==index);
    setComments(tempList);
  }

  function delBtn(id,index) {
    if (uid == id) {
      return <button onClick={() => handleDel(id,index)}>删除</button>
    }
    else {
      return ''
    }
  }
  return (
    <div>
      <div>
        <input type="text" placeholder='发一条友善的评论'></input>
        <button onClick={addComment}>发布</button>
      </div>

      {/* 评论列表 */}
      <div>
        <ul>
          {/* 使用map方法对列表数据进行遍历渲染 */}
          {comments.map((item,index) => (
            <li>{item.content} your uid {item.uid} {delBtn(item.uid,index)}</li>
          ))}
        </ul>
      </div>
    </div>
  );
}

export default App;
```

## 渲染`Tab` + 点击高亮实现

- 需求：点击哪个`Tab`项，哪个做高亮处理
- 核心思路：点击谁就把谁的**`type`(独一无二的标识)记录**下来，与遍历的**每一项的`type`做匹配**，匹配到就负责高亮

```css
span{
  margin: 20px;
  color: #ccc;
}
```

```react
function App() {
  function light(e) {
    const type = e.target
    let div = document.querySelectorAll('div span')
    for (let i = 0; i < div.length; i++) {
      div[i].style.color = '#ccc'
    }
    type.style.color = '#000'
  }
  return (
    <div>
      <div onClick={light}>
        <span>最新</span>
        |
        <span>最热</span>
      </div>
    </div>
  );
}

export default App;
```

## 排序实现

- 需求：点击最新，评论列表按照创建时间倒叙排列（新的在前），点击最热按照点赞数排序（多的在前）

```react
// 导入useState钩子
import { useState } from 'react';

// 评论列表数据
let list = [{
  uid: 1,
  content: '评论1',
  time: '2023-11-11',
  count: 100
},
{
  uid: 2,
  content: '评论2',
  time: '2022-11-11',
  count: 200
},
{
  uid: 3,
  content: '评论5',
  time: '2021-11-11',
  count: 300
}
]

// 当前登录账号的uid
const uid = 123;

function App() {
  // 使用useState维护评论列表
  const [comments, setComments] = useState(list);
  // 定义一个函数，用于添加评论到列表
  function addComment() {
    let comment = document.querySelector('input').value;
    let id = uid
    let count = 1
    let time = '2023-12-27'
    let tempObject = {
      uid: id,
      content: comment,
      count: count,
      time: time
    }
    setComments([...comments, tempObject]);
    document.querySelector('input').value = '';
  }

  function handleDel(id, index) {
    let tempList = comments.filter((item, i) => i !== index);
    setComments(tempList);
  }

  function delBtn(id, index) {
    if (uid == id) {
      return <button onClick={() => handleDel(id, index)}>删除</button>
    }
    else {
      return ''
    }
  }

  function light(e) {
    const type = e.target
    let div = document.querySelectorAll('div span')
    for (let i = 0; i < div.length; i++) {
      div[i].style.color = '#ccc'
    }
    type.style.color = '#000'

    if (type.innerHTML === '最新') {
      // 在使用useState中，要避免修改原来的值，所以不用list，使用[...comments]，不使用list，保证状态的更新渲染
      // 通过localeCompare方法实现按照时间先后顺序比较
      // 不能使用减法，在js中如果无法解析为有效数字的字符串，直接返回NaN而导致无法比较，'2023-11-11'形如时间字符串格式，导致无法正确解析为有效数字的字符串，因为它在时间字符串和普通字符串徘徊而导致无法正确解析为 有效数字的字符串 和 有'-'非数字字符的原因
      setComments([...comments].sort((a, b) => b.time.localeCompare(a.time)))
    } else {
      setComments([...comments].sort((a, b) => b.count - a.count))
    }
  }
  return (
    <div>
      <div onClick={light}>
        <span>最新</span>
        |
        <span>最热</span>
      </div>

      <div>
        <input type="text" placeholder='发一条友善的评论'></input>
        <button onClick={addComment}>发布</button>
      </div>

      {/* 评论列表 */}
      <div>
        <ul>
          {/* 使用map方法对列表数据进行遍历渲染 */}
          {comments.map((item, index) => (
            <li>{item.content} your uid {item.uid} your create time {item.time} your click num {item.count}{delBtn(item.uid, index)}</li>
          ))}
        </ul>
      </div>
    </div>
  );
}

export default App;
```

# 受控表单绑定

使用`React`组件的**状态(`useState`)控制表单的状态**

![受控表单绑定](/images/react/受控表单绑定.png)

```react
import './App.css';
import { useState } from 'react'

function App() {
  const [value, setValue] = useState('')

  return (
    <div className="App">
      {/* {<input></input>} */}

      {/* 表单元素能够自己维护state，根据用户的输入进行更新 ------------------------ 受控组件 */}
      {/* onchange事件：当用户在input输入时执行一段JavaScript代码 */}
      {/* 通过value属性绑定状态，onchange属性绑定状态同步的函数 */}
      {<input type='text' value={value} onChange={(e) => setValue(e.target.value)} />}
    </div>
  );
}

export default App;
```

需要在浏览器中安装`React Developer Tools`插件，然后在开发者工具中的`Components`中查看`State`的变化

# `React`中获取`DOM`

使用`useRef React Hook`钩子函数

- 第一步

使用`useRef`创建`ref`对象，并与`JSX`绑定

`const inputRef = useRef(null)`

`<input type='text' ref={inputRef} />`

- 第二步

 在`DOM`可用下，以事件对象的形式，通过`inputRef.current`拿到`DOM`对象

`console.log(inputRef.current);`

```react
import './App.css';
import { createContext, useContext, useEffect, useRef, useState } from 'react'

function App() {
  const inputRef = useRef(null)
  function getInput() {
    console.log(inputRef.current);
  }

  return (
    <div className="App">
      {/* ref:让不受控制组件的维护变得容易，能够获取DOM节点或React元素实例的工具。允许用户访问 DOM 节点或者在 render 方法中创建的React元素 */}
      {/* 应用场景 */}
      {/* 1、对DOM 元素焦点的控制、内容选择或者媒体播放； */}
      {/* 2、通过对DOM元素控制，触发动画特效； */}
      <input type='text' ref={inputRef} />
      <button onClick={getInput}>点击我获取input的dom元素</button>
    </div>
  );
}

export default App;
```

# 组件通信

**组件之间的数据传递**

![组件通信](/images/react/组件通信.png)

## 父传子 - 基础实现

- 实现步骤
  1. 父组件**传递**数据 `-` **在子组件标签上绑定属性**
  2. 子组件**接收**数据 `-` 子组件通过**`props`参数**接收数据

```react
import './App.css';

function App() {
  const name = 'this is app name'
  function Son(props) {
    console.log(props);
    return <div>this is Son name</div>
  }

  return (
    <div className="App">
      <Son
        name={name}
        age={20}
        isTrue={false}
        list={['Vue', 'React']}
        obj={{ name: 'jack' }}
        cb={() => console.log(123)}
        child={<span>this is span child</span>}
      ></Son>
    </div>
  );
}

export default App;
```

- 注意
  - 组件**只能读取`props`中的数据**
  - props参数名是一个自定义参数，它接收父组件传递的数据

## 父传子 - 特殊的`prop children`

使用场景：当把内容嵌套在子组件标签中，父组件会自动在名为`children`的`prop`属性中接收该内容

```react
import './App.css';
import { createContext, useContext, useEffect, useRef, useState } from 'react'

function App() {
  const name = 'this is app name'
  function Son(props) {
    console.log(props);
    return <div>this is Son name</div>
  }

  return (
    <div className="App">
      <Son>
        <span>这是一个span标签</span>
      </Son>
    </div>
  );
}

export default App;
```

## 父子组件通信 - 子传父

- 核心思路：在**子组件**中**调用父组件中的函数**并**传递参数**

```react
import './App.css';

function App() {
  // 父组件函数
  const getMsg = (msg) => console.log(msg)
  // 通过对象模型解构获取getMs
  function Son({ onGetMsg }) {
    const sonMsg = 'this is son msg'
    return (
      <div>
        <button onClick={() => onGetMsg(sonMsg)}>send</button>
      </div>
    )
  }

  return (
    <div className="App">
      {/* 子组件调用父组件函数 */}
      <Son onGetMsg={getMsg}></Son>
    </div>
  );
}

export default App;
```

## 使用状态提升实现兄弟组件通信

- 实现思路：通过父组件进行兄弟组件之间的数据传递
  1. `A`组件通过**子传父**把数据传给父组件`App`
  2. `App`拿到数据通过**父传子**传递给`B`组件

```react
import './App.css';
import { createContext, useContext, useEffect, useRef, useState } from 'react'

function App() {
  const getMsg = (msg) => {
    console.log(msg);
    setMsg(msg)
  }
  const [msg, setMsg] = useState('')
  function SonA({ onGetAMsg }) {
    const SonAMsg = 'this is A name'
    return (
      <div>
        <button onClick={() => onGetAMsg(SonAMsg)}>send</button>
      </div>
    )
  }
  function SonB(props) {
    console.log(props);
  }

  return (
    <div className="App">
      <SonA onGetAMsg={getMsg}></SonA>
      <SonB msg={msg}></SonB>
    </div>
  );
}

export default App;
```

以下是错误的写法

```react
function SonB(props) {
  console.log(props);
}
/** 为什么这种方法不能够输出console.log(props)？ */
const getMsg = (msg) => { return <SonB getMsgApp={msg}></SonB> }
function SonA({ onGetAMsg }) {
  const SonAMsg = 'this is A name'
  return (
    <div>
      <button onClick={() => onGetAMsg(SonAMsg)}>send</button>
    </div>
  )
 }
```

这段代码不能实现兄弟组件通信的原因是，没有共享状态机制，共享状态机制可以通过useState等实现

## 使用`Context`机制跨层级组件通信

![Context](/images/react/Context.png)

- 实现步骤
  - 使用`createContext`方法创建一个上下文对象`Ctx`
  - 在顶层组件`App`中使用**`Ctx.Provider`组件**提供数据
  - 在底层组件`B`中使用`useContext`钩子函数获取数据

```react
import './App.css';
import { createContext, useContext, useEffect, useRef, useState } from 'react'

function App() {
  const Ctx = createContext()

  const msg = 'this is app name'

  function A() {
    return (
      <div>
        this is A app
        <B />
      </div>
    )
  }

  function B() {
    // 传入上下文对象
    const getMsg = useContext(Ctx)
    return (
      // 获取数据
      <div>this is B app,{getMsg}</div>
    )
  }

  return (
    <div className="App">
      {/* 提供数据 */}
      <Ctx.Provider value={msg}>
        this is App
        <A />
      </Ctx.Provider>
    </div>
  );
}

export default App;
```

# `useEffect`的使用

## `useEffect`的概念理解

**`useEffect`**是一个`React Hook`函数，**用于**在`React`组件中创建不是由事件引起，而是**渲染本身引起的操作（副作用）**，比如：**发送`AJAX`请求，更改`DOM`**等等

注意：不发生任何用户事件，**组件渲染完毕之后**，向服务器要数据

## `useEffect`的基础使用

- 语法：`useEffect(() => {  } , [])`
  - 参数1：一个副作用函数，**函数内部放置要执行的操作**
  - 参数2：可选参数，**若为空数组，副作用函数在组件渲染完毕之后执行一次**

提供案例**需求：在组件渲染完毕之后，立刻从服务端获取频道列表数据并显示到页面中**

接口测试地址：`http://geek.itheima.net/v1_0/channels`

```json
{"data":{"channels":[{"id":0,"name":"推荐"},{"id":1,"name":"html"},{"id":2,"name":"开发者资讯"},{"id":4,"name":"c++"},{"id":6,"name":"css"},{"id":7,"name":"数据库"},{"id":8,"name":"区块链"},{"id":9,"name":"go"},{"id":10,"name":"产品"},{"id":11,"name":"后端"},{"id":12,"name":"linux"},{"id":13,"name":"人工智能"},{"id":14,"name":"php"},{"id":15,"name":"javascript"},{"id":16,"name":"架构"},{"id":17,"name":"前端"},{"id":18,"name":"python"},{"id":19,"name":"java"},{"id":20,"name":"算法"},{"id":21,"name":"面试"},{"id":22,"name":"科技动态"},{"id":23,"name":"js"},{"id":24,"name":"设计"},{"id":25,"name":"数码产品"},{"id":26,"name":"软件测试"}]},"message":"OK"}
```

```react
import './App.css';
import { createContext, useContext, useEffect, useRef, useState } from 'react'

function App() {
  const URL = 'http://geek.itheima.net/v1_0/channels'
  const [list, setList] = useState([])
  useEffect(() => {
    async function getLists() {
      const res = await fetch(URL)
      const lists = await res.json();
      console.log(lists);
      setList(lists.data.channels)
    }
    getLists()
  }, [])

  return (
    <div className="App">
      <span>this is App</span>
      <ul>
        {list.map(item => <li key={item.id}>{item.name}</li>)}
      </ul>
    </div>
  );
}

export default App;
```

## `useEffect`依赖项参数说明

根据**传入依赖项的不同**，会有不同的执行表现

![useEffect](/images/react/useEffect.png)

## `useEffect` — 清除副作用

**组件卸载时自动执行**

需求：在`Son`组件渲染时开启计时器，卸载时清除这个计时器

```react
import './App.css';
import { createContext, useContext, useEffect, useRef, useState } from 'react'

function App() {
  const [time, setTime] = useState(true)
  function Son() {
    useEffect(() => {
      const timer = setInterval(() => {
        console.log('定时器启动中……');
      }, 1000)

      return () => {
        clearInterval(timer)
      }
    }, [])
    return <div>this is son </div>
  }

  return (
    <div className="App">
      {/* 这里的&&并不是字符串，而是用来通过 条件渲染来控制 计时器的开启与卸载 */}
      {time && <Son />}
      <button onClick={() => setTime(false)}>点击我关闭计时器</button>
    </div>
  );
}

export default App;
```

# 自定义`Hook`实现

自定义`Hook`以**`use`打头的函数**，用来实现**逻辑的封装和复用**

![Hook](/images/react/Hook.png)

# `React Hooks`使用规则

**不能嵌套在`if`、`for`、其他函数中**

# 案例：优化B站评论案例

## 优化需求

- 使用**请求接口的方法获取评论列表并渲染**
- 使用**自定义`Hook`函数封装数据请求的逻辑**
- 把评论中的**每一项抽象成一个独立的组件实现渲染**

## 优化需求 - 通过接口获取评论列表

- 实现步骤
  1. 使用`json-server`工具模拟接口服务，通过`axios`发送接口请求
     - `json-server`以`.json`文件作为数据源模拟接口服务的工具
     - `axios`是前端请求库
  2. 使用`useEffect`调用接口获取数据
- 准备工作
  - 在项目中安装`json-server`，这里假设自己的工程目录为`react-basic`
    - 在终端运行`npm i json-server -D`安装`json-server`
    - 在`package.json`文件中添加`"serve": "json-server db.json --port 3004"`
    - 在终端运行`npm run serve`
    - 在浏览器打开`Resources`下的连接查看数据
  - 在项目中安装`axios`
    - 在终端运行`npm install axios`命令安装`axios`
    - 在`App.js`文件中导入`axios`

在安装`json-server`过程中，会影响三处地方，工程目录图

![json-server](/images/react/B站_json-server.png)

![server1](/images/react/server_2.png)

![server1](/images/react/server_3.png)

安装`axios`

![axios](/images/react/axios.png)

`db.json`数据一栏

```json
{
    "list": [
        {
            "uid": 1,
            "content": "评论1",
            "time": "2023-11-11",
            "count": 100
        },
        {
            "uid": 2,
            "content": "评论2",
            "time": "2022-11-11",
            "count": 200
        },
        {
            "uid": 3,
            "content": "评论5",
            "time": "2021-11-11",
            "count": 300
        }
    ]
}
```

```react
import './App.css';
import { createContext, useContext, useEffect, useRef, useState } from 'react'
// 安装axios后要导入
import axios from 'axios'

function App() {
  // 使用useState维护评论列表
  // const [comments, setComments] = useState(list);

  // 通过接口获取评论列表
  const [comments, setComments] = useState([]);
  useEffect(() => {
    async function getLists() {
      // 接口获取数据
      const res = await axios.get('http://localhost:3004/list')
      const data = await res.data
      setComments(data)
      console.log(data);
    }
    getLists()
  }, [])

  return (
    <div className="App">

    </div>
  );
}

export default App;
```

## 优化需求 - 自定义`Hook`函数封装数据请求

- 实现步骤
  1. 编写一个`use`打头的函数
  2. 函数内部编写封装的逻辑
  3. `return`出去组件中用到的状态和方法
  4. 组件中调用函数，解构赋值使用

```jsx
import './App.css';
import { createContext, useContext, useEffect, useRef, useState } from 'react'

function App() {
  // Hook函数封装数据请求
  function useListData() {
    // 通过接口获取评论列表
    const [comments, setComments] = useState([]);
    useEffect(() => {
      async function getLists() {
        // 接口获取数据
        const res = await axios.get('http://localhost:3004/list')
        const data = await res.data
        setComments(data)
        console.log(data);
      }
      getLists()
    }, [])
    return {
      comments, setComments
    }
  }

  const { comments, setComments } = useListData()

  return (
    <div className="App">

    </div>
  );
}

export default App;
```

## 优化需求 - 封装评论项`Item`组件

需求：`App`作为“智能组件”负责数据的获取，`Item`作为“`UI`组件”负责数据的渲染

```jsx
import './App.css';
import { createContext, useContext, useEffect, useRef, useState } from 'react'

function App() {
  // 封装评论项Item组件
  // 函数组件的形参需要是对象
  function Item({ item, index }) {
    return (
      <li>{item.content} your uid {item.uid} your create time {item.time}
        your click num {item.count}{delBtn(item.uid, index)}</li>
    )

  }

  return (
    <div className="App">
      {/* 评论列表 */}
      <div>
        <ul>
          {/* 使用map方法对列表数据进行遍历渲染 */}
          {comments.map((item, index) => (
            <Item item={item} index={index} />
          ))}
        </ul>
      </div>
    </div>
  );
}

export default App;
```

**B站评论案例优化完整代码展示**

```jsx
// 导入useState钩子
import { useEffect, useState } from 'react';
// 安装axios后要导入
import axios from 'axios'

// 当前登录账号的uid
const uid = 123;

function App() {

  // Hook函数封装数据请求
  function useListData() {
    // 通过接口获取评论列表
    const [comments, setComments] = useState([]);
    useEffect(() => {
      async function getLists() {
        // 接口获取数据
        const res = await axios.get('http://localhost:3004/list')
        const data = await res.data
        setComments(data)
        console.log(data);
      }
      getLists()
    }, [])
    return {
      comments, setComments
    }
  }

  const { comments, setComments } = useListData()

  // 封装评论项Item组件
  function Item({ item, index }) {
    return (
      <li>{item.content} your uid {item.uid} your create time {item.time}
        your click num {item.count}{delBtn(item.uid, index)}</li>
    )

  }

  // 定义一个函数，用于添加评论到列表
  function addComment() {
    let comment = document.querySelector('input').value;
    let id = uid
    let count = 1
    let time = '2023-12-27'
    let tempObject = {
      uid: id,
      content: comment,
      count: count,
      time: time
    }
    setComments([...comments, tempObject]);
    document.querySelector('input').value = '';
  }

  function handleDel(id, index) {
    let tempList = comments.filter((item, i) => i !== index);
    setComments(tempList);
  }

  function delBtn(id, index) {
    if (uid == id) {
      return <button onClick={() => handleDel(id, index)}>删除</button>
    }
    else {
      return ''
    }
  }

  function light(e) {
    const type = e.target
    let div = document.querySelectorAll('div span')
    for (let i = 0; i < div.length; i++) {
      div[i].style.color = '#ccc'
    }
    type.style.color = '#000'

    if (type.innerHTML === '最新') {
      // 使用[...comments]，不使用list，保证状态的更新渲染
      // 在使用useState中，要避免修改原来的值，所以不用list
      // 通过localeCompare方法实现按照时间先后顺序比较
      // 不能使用减法，在js中如果无法解析为有效数字的字符串，直接返回NaN而导致无法比较，'2023-11-11'形如时间字符串格式，导致无法解析为有效数字的字符串
      setComments([...comments].sort((a, b) => b.time.localeCompare(a.time)))
    } else {
      setComments([...comments].sort((a, b) => b.count - a.count))
    }
  }
  return (
    <div>
      <div onClick={light}>
        <span>最新</span>
        |
        <span>最热</span>
      </div>

      <div>
        <input type="text" placeholder='发一条友善的评论'></input>
        <button onClick={addComment}>发布</button>
      </div>

      {/* 评论列表 */}
      <div>
        <ul>
          {/* 使用map方法对列表数据进行遍历渲染 */}
          {comments.map((item, index) => (
            <Item item={item} index={index} />
          ))}
        </ul>
      </div>
    </div>
  );
}

export default App;
```

# `Redux`介绍

> `Redux` 是React最常用的集中状态管理工具，可以独立于框架运行

![image.png](./images/react/1.png)

# `Redux`快速体验

## 实现计数器

- 需求：**不和任何框架绑定**，不使用任何构建工具，使用`Redux`实现计数器

![UI图](/images/react/2.png)

- 实现步骤
  1. 引入`Redux`库(`https://cdnjs.cloudflare.com/ajax/libs/redux/4.1.1/redux.min.js`)
  2.  定义一个函数，用来作**返回修改状态** 并 作**值的修改处理**，如：+的状态
  3. 使用`Redux`的`createStore`方法传入函数，生成实例对象
  4. 使用实例方法`subscribe`监听数据的变化，通过实例方法`getState`获取变化后的对象，并且将最新的状态的数据更新到视图中
  5. 使用实例方法`dispatch`提交`action`对象，触发数据变化

```html
<!DOCTYPE html>
<html lang="en">

<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>计时器</title>
    <!-- 引入Redux库 -->
    <script src="https://cdnjs.cloudflare.com/ajax/libs/redux/4.1.1/redux.min.js"></script>
</head>

<body>
    <button id="del">-</button>
    <span>0</span>
    <button id="add">+</button>

    <script>
        // 定义reducer函数,用来返回修改的状态
        function deleteReducer(state = { count: 0 }, action) {
            switch (action.type) {
                case 'add':
                    return { count: state.count + 1 }
                case 'del':
                    return { count: state.count - 1 }
                default:
                    return state
            }
        }

        // 创建一个Redux store来保存计数器的状态
        const store = Redux.createStore(deleteReducer)

        // 使用store的subscribe方法来订阅状态的变化
        store.subscribe(() => {
            console.log('状态更新:', store.getState());
            document.querySelector('span').innerText = store.getState().count
        })

        // 使用store的dispatch方法来提交action对象,触发状态的修改
        document.getElementById('add').addEventListener('click', function () {
            store.dispatch({ type: 'add' })
        })

        document.getElementById('del').addEventListener('click', function () {
            store.dispatch({ type: 'del' })
        })
    </script>
</body>

</html>
```

## `Redux`数据流架构

![redux](/images/react/redux.png)

1. `state`：一个对象，存放管理的数据
2. `action`：一个对象，存放将要调用的功能的类型
3. `reducer`：一个函数，根据`action`提供的类型来调用对应的操作

# `Redux`与`React `- 环境准备

## 配套工具

![react-redux](/images/react/4.png)

## 配置基础环境

1. 创建React项目

`npx create-react-app react-redux `

2. 安装配套工具

`npm i @reduxjs/toolkit  react-redux`

3. 启动项目

`npm run start `

## store目录结构设计

在src目录下创建如下内容

![content](/images/react/5.png)

# `Redux`与`React` - 实现`counter`

## 整体路径熟悉

![6](/images/react/6.png)

## 使用React Toolkit 创建counterStore

配置counterStore模块

```react
import { createSlice } from '@reduxjs/toolkit'

const counterStore = createSlice({
    // 模块名唯一
    name: 'counter',
    // 初始数据
    initialState: {
        count: 0
    },
    // 修改数据的同步方法
    reducers: {
        increment: state => { state.count++ },
        decrement: state => { state.count-- }
    }
})

// 解构出actionCreater
const { increment, decrement } = counterStore.actions

const counterReducer = counterStore.reducer

// 导出解构了actionCreater的数据
export { increment, decrement }
// 导出reducer函数
export default counterReducer
```

配置index.js文件

```react
import { configureStore } from "@reduxjs/toolkit";

import counterReducer from "./modules/counterStore";

export default configureStore({
    reducer: {
        // 注册子模块
        counter: counterReducer
    },
})
```

## 为react注入store

通过`react-redux`内置组件`Provider`，将`Redux`和`React`进行连接，通过`store`参数把创建好的`store`实例注入进应用，实现`Redux store`与`React`的连接建立

配置index.js

```react
import React from 'react';
import ReactDOM from 'react-dom/client';
import './index.css';
import App from './App';
// 导入store
import store from './store';
// 导入store提供的组件Provider
import { Provider } from 'react-redux';
import reportWebVitals from './reportWebVitals';

const root = ReactDOM.createRoot(document.getElementById('root'));
root.render(
  <React.StrictMode>
    <Provider store={store}>
      <App />
    </Provider>
  </React.StrictMode>
);
```

## React组件使用store中的数据

通过`useSelector`钩子函数，将store中的数据映射到组件中

![7](/images/react/7.png)

## React组件修改store中的数据

通过hook函数：`useDispatch`修改store中的数据

`useDispatch`：生成提交action对象的dispatch函数

```react
import './App.css';
import { useDispatch, useSelector } from 'react-redux';
import { decrement, increment } from './store/modules/counterStore'

function App() {

  // 注意这里一定是对象
  const { count } = useSelector((state) => state.counter)

  const dispatch = useDispatch()

  return (
    <div className="App">
      <button onClick={() => dispatch(decrement())}>-</button>
      <span>{count}</span>
      <button onClick={() => dispatch(increment())}>+</button>
    </div>
  );
}

export default App;
```

# `Redux`与React - 提交action传参

- 需求：组件中有两个按钮`add to 10`和`add to 20`，能够把count值修改到对应的数字，目标count值需要在组件中传递，需要提交action时传递参数

- 实现方式

  - 在reducers对象中添加函数，实现把count值修改到对应数字的功能，并且添加action对象参数
  - 解构并导出该函数
  - 调用dispatch提交action对象，并传递参数，此时参数会传递到action对象中的payload属性上

  counterStore配置中的修改

  ```react
  reducers: {
  	increment: state => { state.count++ },
  	decrement: state => { state.count-- },
      // 在reducers中添加函数
  	addToNum: (state, action) => { state.count = action.payload }
      }
  // 解构并导出addToNum函数
  const { increment, decrement, addToNum } = counterStore.actions
  export { increment, decrement, addToNum }
  ```

  App.js的配置

  ````react
  import './App.css';
  import { useDispatch, useSelector } from 'react-redux';
  import { addToNum } from './store/modules/counterStore'
  
  function App() {
  
    // 注意这里一定是对象
    const { count } = useSelector((state) => state.counter)
  
    const dispatch = useDispatch()
  
    return (
      <div className="App">
        <span>{count}</span>
        <button onClick={() => dispatch(addToNum(10))}>add to 10</button>
        <button onClick={() => dispatch(addToNum(20))}>add to 20</button>
      </div>
    );
  }
  
  export default App;
  ````
