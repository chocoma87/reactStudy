#State
컴퍼넌트 안에서 지정해 준다. props와 비슷하지만, 해당 컴포넌트에서만 접할 수 있는 private 오브젝트이다. class로 생성된 컴포넌트만이 가지고 있는 기능으로 local state 이다. props을 사용할 건지, state를 사용할 것인지는 상황에 따라 결정한다.  

클래스가 아닌 컴포넌트의 예는 다음과 같다.

```javascript
function TitleComponent (props){
    return (
        <div>{props.time}</div>
    )
}

ReactDOM.render(<TitleComponent time={new Date().toLocaleTimeString()} />, document.querySelector('.header-title'));
```


##state basic
```javascript
var TodoComponent = React.createClass({
    getInitialState: function (){
        return {
            todo: ["eat", "study", "sleep"]
        }
    },
    render: function(){
        return (
            <div>
                {this.state.todo[0]}
            </div>
        );
    }
});
```
컴포넌트에서 this.state로 접근할 수 있다.

```javascript
// create component
var TodoComponent = React.createClass({
    getInitialState: function (){
        return {
            todo: ["eat", "study", "sleep"],
            age: 30
        }
    },
    render: function(){

        var timeout = setTimeout(function (){
            this.setState({
                age: 40
            });
        }.bind(this), 3000);

        return (
            <div>
                <div>
                    {this.state.age}
                </div>
                <div>
                    {this.props.profile.name}
                </div>
            </div>
        );
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

setState 함수로 state값을 바꿀 수 있다.

##setState
```javascript
setState(nextState, callback)
```


nextState 에는 오브젝트 또는 오브젝트를 반환하는 함수가 올 수 있다.setState 함수 실행 후에는 항상 rerender 된다. 


##cycling state
```javascript
// create component
var TodoComponent = React.createClass({
    getInitialState: function (){
        return {
            todo: ["eat", "study", "sleep"],
            age: 30
        }
    },
    render: function(){

        var todos = this.state.todo;
        todos = todos.map(function(value, index){
            return (
                <span key={value.toString()} id={value.toString()}>{value}</span>
            );
        });

        return (
            <div>
                {todos}
            </div>
        );
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
map 함수를 사용해서 jsx를 포함한 어레이로 바꿔준다. 이때 각 리스트 아이템은 리액트가 식별할 수 있는 key 값이 있어야 한다.(브라우저에서는 출력되지 않고, 리액트 인스펙터에서 확인할 수 있다.)


##props와 state의 차이점
props는 컴포넌트에서 변경할 수 없는 오브젝트이고 반면에 state는 컴포넌트 안에서 변경할 수 있는 오브젝트이다. props는 컴포넌트를 render로 실행시킬 때 부모로부터 컴포넌트로 넘겨지는 값이고, state는 컴포넌트 안에서 정의되며 사용 할 수 있는 오브젝트이다. 
다이나믹하게 변경되어야 하는 컨텐츠의 경우 state를 사용하면 된다. 아래는 리액트 도큐먼테이션에서 강조하고 있는 문장이다. 여기서 [pure functon](https://en.wikipedia.org/wiki/Pure_function)은 같은 인풋을 받았을 때 항상 같은 아웃풋을 내는 함수를 말한다.  
**All React components must act like pure functions with respect to their props.**


###what is state?
state muchine 이라는 컴퓨터공학 분야에서 나왔다고 한다. 프로그램이 실행되고 있는 현재 사이클에서 정의되고 사용되고 있는 모든 변수의 snapshot이라고 할 수 있다.
