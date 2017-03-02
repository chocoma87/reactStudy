#Child component

```
// create component
var TodoComponent = React.createClass({
    getInitialState: function (){
        return {
            todo: ["eat", "study", "sleep"],
            age: 30
        }
    },
    render: function(){
        let todos = this.state.todo;
        todos = todos.map(function (item, index){
            return (
                <TodoItem value = {item} key = {index} />
            )
        });

        return (
            <div>{todos}</div>
        );
    }
});


// child component
var TodoItem = React.createClass({
    render: function (){
        return (
            <span><strong>{this.props.value}</strong></span>
        )
    }
});

var profile = {
    name: "shinwoo",
    age: 30,
    address: "seoul"
}

// put component into html page
ReactDOM.render(<TodoComponent day="목" profile={profile} />, document.querySelector(".header-title"));
```



이때, 자식 컴포넌트에서는 부모 컴포넌트의 state에 접근할 수 없다.

자식 컴포넌트에서 부모 컴포넌트의 데이터에 접근할 수 있는 방법이 있는데, 부모 컴포넌트에서 자신의 데이터를 가공하는 함수를 만든 다음 함수를 자식 컴포넌트에 props로 넘겨주면 된다. 이때, this등가 참조하는 값이 무엇인지 주의해야 한다.
```
// 부모 class App extends React.Component {
    constructor (props){
        super(props);
        this.state = {
            login: 0
        }
    }

    changeState (value){
        this.setState({
            login: value
        });
    }

    render (){
        return (
            <div>
                <Header googleApi = {this.props.googleApi} isSignIn = {this.props.isSignIn} changeState = {this.changeState.bind(this)} />
                <div className="mainContents"></div>
            </div>
        )
    }
}

// 자식 컴포넌트
class LoginBtn extends React.Component {
    constructor (props){
        super(props);
        this.state = {
            signed: this.props.isSignIn ? 1 : 0,
            text: ["로그인", "로그아웃"],
            eventHandler: [this.signIn, this.signOut]
        };
    }

    signIn (){
        this.props.googleApi.signIn();
        this.props.changeState(1);

        // 로그인 state를 바꿔준다.
        this.setState({
            signed: 1
        });
    }

    signOut (){
        this.props.googleApi.signOut();
        this.props.changeState(0);

        // 로그인 state를 바꿔준다.
        this.setState({
            signed: 0
        });
    }

    render (){
        let index = this.state.signed;

        return (
            <button id="authorize-button" className="button" onClick={this.state.eventHandler[index].bind(this)}>
                {this.state.text[index]}
            </button>
        )
    }
}
```
