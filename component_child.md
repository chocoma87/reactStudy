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

