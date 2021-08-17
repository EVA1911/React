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
