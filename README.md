## 1. JSX
JSX，是一个 JavaScript 的语法扩展，也是一个表达式，在编译之后，JSX 表达式会被转为普通 JavaScript 函数调用，并且对其取值后得到 JavaScript 对象。  
`const element = <h1>Hello, world!</h1>;`  
可以在 if 语句和 for 循环的代码块中使用 JSX，将 JSX 赋值给变量，把 JSX 当作参数传入，以及从函数中返回 JSX：  
```
function getGreeting(user) {  
  if (user) {  
    return <h1>Hello, {formatName(user)}!</h1>;  
  }  
  return <h1>Hello, Stranger.</h1>;  
}
```
假如一个标签里面没有内容，你可以使用 /> 来闭合标签，就像 XML 语法一样：  
`const element = <img src={user.avatarUrl} />;`  
在属性中嵌入 JavaScript 表达式时，不要在大括号外面加上引号。你应该仅使用引号（对于字符串值）或大括号（对于表达式）中的一个，对于同一属性不能同时使用这两种符号。  
  
Babel 会把 JSX 转译成一个名为 React.createElement() 函数调用。  
以下两种示例代码完全等效：  
```
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
```  
```
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```
  
React 元素是不可变对象。一旦被创建，你就无法更改它的子元素或者属性。一个元素就像电影的单帧：它代表了某个特定时刻的 UI。根据我们已有的知识，更新 UI 唯一的方式是创建一个全新的元素，并将其传入 ReactDOM.render()。 
  
React 只更新它需要更新的部分:React DOM 会将元素和它的子元素与它们之前的状态进行比较，并只会进行必要的更新来使 DOM 达到预期的状态。  
  
所有 React 组件都必须像纯函数一样保护它们的 props 不被更改。  
  
## 2. 生命周期  
在具有许多组件的应用程序中，当组件被销毁时释放所占用的资源是非常重要的。当组件第一次被渲染到 DOM 中的时候，就为其设置一个计时器。这在 React 中被称为“挂载（mount）”。同时，当 DOM 中组件被删除的时候，应该清除计时器。这在 React 中被称为“卸载（unmount）”。  
我们可以为 class 组件声明一些特殊的方法，当组件挂载或卸载时就会去执行这些方法，这些方法叫做“生命周期方法”。  
  
## 3.组件&Props
当 React 元素为用户自定义组件时，它会将 JSX 所接收的属性（attributes）以及子组件（children）转换为单个对象传递给组件，这个对象被称之为 “props”。  
例如，这段代码会在页面上渲染 “Hello, Sara”：
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```
我们调用 ReactDOM.render() 函数，并传入`<Welcome name="Sara" />`作为参数。
React调用 Welcome 组件，并将 `{name: 'Sara'}` 作为 props 传入。
Welcome 组件将 `<h1>Hello, Sara</h1>` 元素作为返回值。
React DOM 将 DOM 高效地更新为`<h1>Hello, Sara</h1>`。
组件名称必须以大写字母开头。  
  
我们可以创建一个可以多次渲染 Welcome 组件的 App 组件：
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

function App() {
  return (
    <div>
      <Welcome name="Sara" />
      <Welcome name="Cahal" />
      <Welcome name="Edite" />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```
  
组件无论是使用函数声明还是通过 class 声明，都决不能修改自身的 props。所有 React 组件都必须像纯函数一样保护它们的 props 不被更改。  
  
State 与 props 类似，但是 state 是私有的，并且完全受控于当前组件。  
通过以下五步将 Clock 的函数组件转成 class 组件：  
创建一个同名的 ES6 class，并且继承于 React.Component。
添加一个空的 render() 方法。
将函数体移动到 render() 方法之中。
在 render() 方法中使用 this.props 替换 props。
删除剩余的空函数声明。  
  
我们通过以下三步将 date 从 props 移动到 state 中：  
把 render() 方法中的 this.props替换成 this.state：  
添加一个 class 构造函数，然后在该函数中为 this.state 赋初值：  

