## Demo1

新建 index.html

```html
<!DOCTYPE html>
<html>
  <head>
    <meta charset="UTF-8" />
    <title>Hello Wilmar</title>
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>
    <script src="https://unpkg.com/babel-standalone@6.15.0/babel.min.js"></script>
  </head>
  <body>
    <div id="root"></div>
    <script type="text/babel">

      ReactDOM.render(
        <h1>Hello, Wilmar!</h1>,
        document.getElementById('root')
      );

    </script>
  </body>
</html>
```

## Demo2: JSX

```javascript
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Wilmar',
  lastName: 'Shanghai'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```
```
    Hello, {user.firstName} {user.lastName}!
```
属性写法、className
```
  <h1 style={{color: 'red'}} className="hello">
```

## Demo3：只渲染变化部分
```
function tick() {
  const element = (
    <div>
      <h1>Hello, Wilmar!</h1>
      <h2>北京时间：{new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```
如果是JavaScript
```
    <script type="text/JavaScript">
function tick() {
  const element = ('\
    <div>\
      <h1>Hello, Wilmar!</h1>\
      <h2>北京时间：'+new Date().toLocaleTimeString()+'.</h2>\
    </div>'
  );
    document.getElementById('root').innerHTML = element;
}

setInterval(tick, 1000);
```


## Demo4：组件

简单版：
```
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```
class
```
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}

ReactDOM.render(
    <Welcome name="Jon">
    </Welcome>,
    document.getElementById("root")
)
```
也可以
```
const element = <Welcome name="Sara" />;
ReactDOM.render(
  element,
  document.getElementById('root')
);
```

负责一点的
```
function formatDate(date) {
  return date.toLocaleDateString();
}

function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
             src={props.author.avatarUrl}
             alt={props.author.name} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}

const comment = {
  date: new Date(),
  text: 'I hope you enjoy learning React!',
  author: {
    name: 'Hello Kitty',
    avatarUrl: 'http://placekitten.com/g/64/64'
  }
};
ReactDOM.render(
  <Comment
    date={comment.date}
    text={comment.text}
    author={comment.author} />,
  document.getElementById('root')
);
```

分解 comment
```

function Avatar(props) {
  return (
    <img className="Avatar"
         src={props.user.avatarUrl}
         alt={props.user.name} />
  );
}

function UserInfo(props) {
  return (
    <div className="UserInfo">
      <Avatar user={props.user} />
      <div className="UserInfo-name">
        {props.user.name}
      </div>
    </div>
  );
}

function Comment(props) {
  return (
    <div className="Comment">
      <UserInfo user={props.author} />
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```



去 https://github.com/facebook/react/releases 下载 react.development.js，react-dom.development.js