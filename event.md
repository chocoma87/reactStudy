#Event

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
                <TodoItem value = {item} key = {index} clickedFnc = {this.deleteFnc} />
            )
        }.bind(this));

        return (
            <div>{todos}</div>
        );
    },

    deleteFnc: function (item){
        let newTodo = this.state.todo.filter(function (value, index){
            return value !== item;
        });

        this.setState({
            todo: newTodo
        })
    }
});

// child component
var TodoItem = React.createClass({
    render: function (){
        return (
            <span><strong onClick = {this.clicked}>{this.props.value}</strong></span>
        )
    },

    clicked: function (){
        this.props.clickedFnc(this.props.value);
    }

});

// put component into html page
ReactDOM.render(<TodoComponent />, document.querySelector(".header-title"));
```

html테그에 인라인으로 이벤트 헨들러 붙여주는 것처럼 onClick 속성을 추가해주면 된다. 이때 부모 컴포넌트와 자식 컴포넌트사이에 통신을 주고받는게 문제가 되는데, 자식이 부모 컴포넌트의 
state를 변경해 주기 위해서는 부모 컴포넌트에 함수를 만들어 놓고 자식 컴포넌트에 props으로 넘겨주면 된다. 이때 역시 문제가 되는게 this 바인딩인데, map 함수를 사용할 때 bind 메소드를 써줘야 한다. 자식 컴포넌트로 넘겨진 함수의 this 바인딩은 리액트에서 더 효과적인 방법으로 알아서 해준다고 한다.

그리고 인상적인게 위 코드에서 클릭된 span 테그가 삭제되는 이벤트를 작성하였는데, 코드에서는 전혀 dom을 삭제하는 코드 없이 state의 todo 어레이만 수정해 주는 것으로 dom삭제 동작이 가능하게 된다. 

###주의 
state를 변경할 때는 반드시 this.setState 함수를 사용해야 한다. this.state = "" 방식으로 하면 re-render 되지 않는다.
