# React 教程

yinguowei 2018-02

- [官网](https://reactjs.org/)
- [中文版官网](https://doc.react-china.org/)

## 主要模块

Component, State, Props, JSX, Refs

## 01 安装、引用
参考：https://doc.react-china.org/docs/try-react.html

- 可以在线用工具编写，
- 也可以下载模板：[single-file-example.html](https://raw.githubusercontent.com/reactjs/reactjs.org/master/static/html/single-file-example.html)
- https://github.com/facebook/react/releases 下载 release 文件

使用 React

用 npm 安装，或者在 HTML 内引入 js

```html
    <script src="../build/react.js"></script>
    <script src="../build/react-dom.js"></script>
    <script src="../build/browser.min.js"></script>
```

`ReactDOM.render()` 负责将 JSX 翻译成 HTML，并插入 DOM 节点

```html
<div id="example"></div>
<script type="text/babel">
  ReactDOM.render(
    <h1>Hello, world!</h1>,
    document.getElementById('example')
  );
</script>
```

## JSX 语法
- `<` 开头是 HTML 代码
- `{` 开头是 JavaScript 代码
- 插入 JavaScript 变量（表达式） `{}`
- 不能使用 if else 语句，可以使用 conditional (三元运算) 表达式来替代`<h1>{i == 1 ? 'True!' : 'False'}</h1>`
- `{/*注释...*/}`
- 数组会自动展开 `<div>{arr}</div>`

## 组件（Component）

创建一个组件，用 `React.createClass`，实现 `render` 方法
```javascript
var HelloMessage = React.createClass({
  render: function() {
    return <h1>Hello {this.props.name}</h1>;
  }
});
```

使用就是直接当 HTML 标签
```javascript
ReactDOM.render(
  <HelloMessage name="John" />,
  document.getElementById('example')
);
```

> 注意
> 1. 组件类的第一个字母必须大写
> 2. 只能包含一个顶层标签
> 3. 特别的，`class` 属性需要写成 `className` ，`for` 属性需要写成 `htmlFor` ，这是因为 `class` 和 `for` 是 JavaScript 的保留字

定义到 js
```javascript
class HelloMessage extends React.Component {
  render() {
    return (
      <div>
        Hello {this.props.name}
      </div>
    );
  }
}
```

新写法
```
const App = () => (
  <div style={styles}>
    <Hello name="CodeSandbox" />
    <h2>Start editing to see some magic happen {'\u2728'}</h2>
  </div>
);
```
### 将函数转换为类
你可以通过5个步骤将函数组件 Clock 转换为类
1. 创建一个名称扩展为 React.Component 的ES6 类
2. 创建一个叫做render()的空方法
3. 将函数体移动到 render() 方法中
4. 在 render() 方法中，使用 this.props 替换 props
5. 删除剩余的空函数声明

## 属性（Props）

将 html 标签的属性转入 `this.props`
- `this.props` 与属性对应
- `this.props.children` 属性表示组件的所有子节点

```JavaScript
var NotesList = React.createClass({
  render: function() {
    return (
      <ol>
      {
        React.Children.map(this.props.children, function (child) {
          return <li>{child}</li>;
        })
      }
      </ol>
    );
  }
});

ReactDOM.render(
  <NotesList>
    <span>hello</span>
    <span>world</span>
  </NotesList>,
  document.body
);
```
## State 

- 不能直接设置 state，要用`this.setState({val: value})`
- 构造函数是唯一能够初始化 this.state 的地方
```
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }
```

state 和 props 的区别：可变、不可变

## 事件处理
```
<button onClick={activateLasers}>
```

- 不能使用返回 false 的方式阻止默认行为。必须明确的使用 preventDefault

## 状态提升
需要共用状态

