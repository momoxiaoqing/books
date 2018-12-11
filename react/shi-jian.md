1、命名：驼峰式

2、语法：

```js
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

3、不能返回false 来阻止默认行为，必须用preventDefault

```js
function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }
```

4、类的方法默认是不会绑定 this 的

```js
<!DOCTYPE html>
<html>
<head>
    <meta charset="UTF-8"/>
    <title>Hello World</title>
    <script src="https://unpkg.com/react@16/umd/react.development.js"></script>
    <script src="https://unpkg.com/react-dom@16/umd/react-dom.development.js"></script>

    <!-- Don't use this in production: -->
    <script src="https://unpkg.com/babel-standalone@6.15.0/babel.min.js"></script>
</head>
<body>
<div id="root"></div>
<script type="text/babel">
    class Clock extends React.Component {
        constructor (props) {
            super(props);
            this.state = {
                date: new Date(),
                posts: [1],
                comments: [1],
                count:1
            };
            this.add=this.add.bind(this) //将add方法绑定到this上；
        }

        //当组件输出到 DOM 后会执行
        componentDidMount () {
            this.timerID = setInterval(() => this.tick(), 1000)
        }

        //卸载计时器：
        componentWillUnmount () {
            clearInterval(this.timerID)
        }

        tick(){
            this.setState({
                date:new Date(),
                posts:[1,2,3]
            })
        }
        add(){
            this.setState((prevState)=>{
                debugger
                count:prevState.count++
            })
        }
        render () {
            return (
                <div>
                    <div>{this.state.count}</div>
                    <div><button onClick={this.add}>add</button></div>
                    //<div><button onClick={this.add()}>add</button></div>  //不管是否绑定add方法，count会随date变化
                    <div>
                        <h1>Hello world !</h1>
                        <h2>It is {this.state.date.toLocaleTimeString()}</h2>
                        <h2>{this.state.posts}</h2>
                        <h2>{this.state.comments}</h2>
                    </div>
                </div>
            )
        }
    }

    ReactDOM.render(
        <Clock/>,
        document.getElementById('root')
    );


</script>
<!--
  Note: this page is a great way to try React but it's not suitable for production.
  It slowly compiles JSX with Babel in the browser and uses a large development build of React.

  Read this section for a production-ready setup with JSX:
  https://reactjs.org/docs/add-react-to-a-website.html#add-jsx-to-a-project

  In a larger project, you can use an integrated toolchain that includes JSX instead:
  https://reactjs.org/docs/create-a-new-react-app.html

  You can also use React without JSX, in which case you can remove Babel:
  https://reactjs.org/docs/react-without-jsx.html
-->
</body>
</html>
```


