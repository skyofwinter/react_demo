This is a collection of simple demos of React.js.
这是React的一些demo code

## Related Projects 相关推荐
- [React Router Tutorial](https://github.com/reactjs/react-router-tutorial)
- [React Demos](https://github.com/ruanyf/react-demos)
- [React Demo](https://github.com/ruanyf/react-testing-demo)


## How to use 怎么使用

First copy the repo into your disk.
首先可选择下载到本地磁盘 或者 本地新建html 复制文件内容
```bash
$ git clone git@github.com:skyofwinter/react_demo.git
```
Then play with the source files under the repo's directory.
然后在浏览器上面运行查看

## HTML Template HTML 模板
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <!--/*1. 选择使用CDN*/-->
    <script src="https://cdn.bootcss.com/react/15.4.2/react.min.js"></script>
    <script src="https://cdn.bootcss.com/react/15.4.2/react-dom.min.js"></script>
    <script src="https://cdn.bootcss.com/babel-standalone/6.22.1/babel.min.js"></script>

    <title>React 学习</title>
</head>
<body>
<div id="dd">

</div>
    <script type="text/babel">
        //** your code !!!
    </script>

</body>
</html>
```

## Index

1. [Hello World](#01-hello)
1. [Hello Names](#02-hello-names)
1. [Use array](#03-use-array)
1. [Define a Function](#04-define-a-function )
1. [Function Children](#05-function-children)
1. [PropTypes](#06-proptypes)
1. [Click Event](#07-click-event)
1. [Define a Class](#08-define-a-class)
1. [State](#09-state)
1. [Component Lifecycle](#10-component-lifecycle)
1. [Ajax](#11-ajax)
1. [Show Stars](#12-show-stars)


---

## 01: Hello World

 [source](https://github.com/skyofwinter/react_demo/blob/master/reactdemo01.html)

```js
ReactDOM.render(
  <h1>Hello, world!</h1>,
  document.getElementById('dd')
);
```
## 02: Hello Names

 [source](https://github.com/skyofwinter/react_demo/blob/master/reactdemo02.html)
```js
const names = ['Alice', 'Emily', 'Kate'];
const items = names.map((name) =>
        <div>hello,{name}!</div>
);

ReactDOM.render(
    <h4>{items}</h4>,
    document.getElementById("dd")
);
```

## 03: Use array

[source](https://github.com/skyofwinter/react_demo/blob/master/reactdemo03.html)

Show an array of JavaScript variable
展示 JavaScript 数组变量
```js
var arr = [
    <h1>Hello world!</h1>,
    <h2>React is awesome</h2>,
];

ReactDOM.render(
        <div>{arr}</div>,
    document.getElementById("dd")
);
```

## 04: Define a Function

[source](https://github.com/skyofwinter/react_demo/blob/master/reactdemo04.html)

Define a simple component, a Function
使用最简单的函数组件
```javascript
function HelloMessage(props) {
    return <h1>Hello {props.name}</h1>;
};

ReactDOM.render(
        <HelloMessage name = 'John'/>,
    document.getElementById("dd")
);
```
## 05: Function Children

[source](https://github.com/skyofwinter/react_demo/blob/master/reactdemo05.html)

React uses `props.children` to access a component's children nodes.
使用props.children 来访问节点
```javascript
function NotesList(props) {
        return(
            <ol>
                {
                    React.Children.map(props.children, function (child) {
                        return <li>{child}</li>;
                    })
                }
            </ol>
        );
};

ReactDOM.render(
    <NotesList>
        <span>hello</span>
        <span>world</span>
    </NotesList>,
    document.getElementById("dd")
);
```

## 06: PropTypes

[source](https://github.com/skyofwinter/react_demo/blob/master/reactdemo06.html)
Use defaultProps and  proptype
使用PropTypes
```javascript
const data = 123;
function MyTitle(props) {
    return (<h1> {props.title} </h1>);
}

MyTitle.defaultProps = {
    title:'default'
}
MyTitle.proptype = {
    title: PropTypes.string,
}

ReactDOM.render(
        <MyTitle title={data}/>,
    document.getElementById("dd")
);
```

## 07: Click Event

[source](https://github.com/skyofwinter/react_demo/blob/master/reactdemo07.html)

```js
function MyComponent (){
    function handleClick(e) {
        console.log("click button");
    }
    return (
        <div>
            <h4>hello world</h4>
            <input type="button" onClick={handleClick} value="button"/>
        </div>
     );

};

ReactDOM.render(
        <MyComponent />,
    document.getElementById("dd")
);
```

## 08: Define a Class

[source](https://github.com/skyofwinter/react_demo/blob/master/reactdemo08.html)
if we need keep a state for Component, then should use class.
如果需要用到组件state，使用class来创建组件

```js
class LikeButton extends React.Component{
    constructor(){
        super();
        this.state = {liked : false};
        this.handleClick = this.handleClick.bind(this);
    }

    handleClick(){
        this.setState(prevState => ({
            liked:!prevState.liked
        }));
        console.log("liked " + this.state.liked)

    }

    render(){
        var text = this.state.liked? ' like ':' don\'t like ';
        return (
            <div>
                <button onClick={this.handleClick}>you {text} it, click to change it!</button>
            </div>
        )
    };
}

ReactDOM.render(
        <LikeButton/>,
    document.getElementById("dd")
);
```


## 09: State

[source](https://github.com/skyofwinter/react_demo/blob/master/reactdemo09.html)

```js
class  InputForm extends React.Component{
    constructor(){
        super();
        this.state = {
            value:'input content!'
        }
        this.handleChange = this.handleChange.bind(this);
    }
    handleChange(event) {
        this.setState({value: event.target.value});
    }

    render() {
        return (
                <div>
                    <input type="text" value={this.state.value} onChange={this.handleChange}/>
                </div>
        );
    }

}


ReactDOM.render(
        <InputForm/>,
    document.getElementById("dd")
);
```

More information on [official document](http://facebook.github.io/react/docs/forms.html).

## 10: Component Lifecycle

[source](https://github.com/skyofwinter/react_demo/blob/master/reactdemo10.html)

```js
class Hello extends React.Component {
    constructor(props) {
        super(props);
        this.state = {
            opacity: 1.0
        }
    }
    componentDidMount() {
        this.timer = setInterval(function () {
            var opacity = this.state.opacity;
            opacity -= .05;
            if (opacity < 0.1) {
                opacity = 1.0;
            }
            this.setState({
                opacity: opacity
            });
        }.bind(this), 100);
    }

    render() {
        return (
                <div style={{opacity: this.state.opacity}}>
                    Hello {this.props.name}
                </div>
        );
    }
}
ReactDOM.render(
        <Hello name="world"/>,
    document.getElementById("dd")
);
```

- **componentWillMount()**: Fired once, before initial rendering occurs. Good place to wire-up message listeners. `this.setState` doesn't work here.
- **componentDidMount()**: Fired once, after initial rendering occurs. Can use `this.getDOMNode()`.
- **componentWillUpdate(object nextProps, object nextState)**: Fired after the component's updates are made to the DOM. Can use `this.getDOMNode()` for updates.
- **componentDidUpdate(object prevProps, object prevState)**: Invoked immediately after the component's updates are flushed to the DOM. This method is not called for the initial render. Use this as an opportunity to operate on the DOM when the component has been updated.
- **componentWillUnmount()**: Fired immediately before a component is unmounted from the DOM. Good place to remove message listeners or general clean up.
- **componentWillReceiveProps(object nextProps)**: Fired when a component is receiving new props. You might want to `this.setState` depending on the props.
- **shouldComponentUpdate(object nextProps, object nextState)**: Fired before rendering when new props or state are received. `return false` if you know an update isn't needed.

## 11: Ajax

[source](https://github.com/skyofwinter/react_demo/blob/master/reactdemo11.html)

Use Ajax to fetch data in the event handler of `componentDidMount`.
使用Ajax获取数据

```js
class UserGist extends React.Component{
    constructor(props){
        super(props);
        this.state = {
            username: '',
            lastGistUrl: ''
        }
    }
    componentDidMount() {
        $.get(this.props.source, function(result) {
            var lastGist = result[0];
                this.setState({
                    username: lastGist.owner.login,
                    lastGistUrl: lastGist.html_url
                });

        }.bind(this));
    }

    render() {
        return (
                <div>
                    {this.state.username}'s last gist is <a href={this.state.lastGistUrl}>here</a>
                </div>
        );
    }
}

ReactDOM.render(
        <UserGist source="https://api.github.com/users/octocat/gists" />,
    document.getElementById("dd")
);
```

## 12: Show Stars

[source](https://github.com/skyofwinter/react_demo/blob/master/reactdemo12.html)

```javascript
ReactDOM.render(
  <RepoList
    promise={$.getJSON('https://api.github.com/search/repositories?q=javascript&sort=stars')}
  />,
  document.getElementById('example')
);
```

The above code takes data from Github's API, and the `RepoList` component gets a Promise object as its property.

Now, while the promise is pending, the component displays a loading indicator. When the promise is resolved successfully, the component displays a list of repository information. If the promise is rejected, the component displays an error message.

```javascript
class RepoList extends React.Component {
    constructor() {
        super();
        this.state = {
            loading: true,
            error: null,
            data: null
        }
    }

    componentDidMount() {
        this.props.promise.then(
            value => this.setState({loading: false, data: value}),
            error => this.setState({loading: false, error: error}));
    }

    render() {
        if (this.state.loading) {
            return <span>Loading...</span>;
        }
        else if (this.state.error !== null) {
            return <span>Error: {this.state.error.message}</span>;
        }
        else {
            var repos = this.state.data.items;
            var repoList = repos.map((repo) =>
                    <li>
                        <a href={repo.html_url}>{repo.name}</a> ({repo.stargazers_count} stars)
                        <br/>
                        {repo.description}
                    </li>
            );
            return (
                    <main>
                        <h1>Most Popular JavaScript Projects in Github</h1>
                        <ol>{repoList}</ol>
                    </main>
            );
        }
    }
};

ReactDOM.render(
        <RepoList promise={$.getJSON('https://api.github.com/search/repositories?q=javascript&sort=stars')}/>,
    document.getElementById("dd")
);
```




## License

BSD licensed
