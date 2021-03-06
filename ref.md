#Ref
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
        let todos = this.state.todo;
        todos = todos.map(function (item, index){
            return (
                <TodoItem value = {item} key = {index} clickedFnc = {this.deleteFnc} />
            )
        }.bind(this));

        return (
            <div>
                <div>{todos}</div>
                <InputComponent whenSubmit = {this.addItem} />
            </div>

        );
    },

    deleteFnc: function (item){
        let newTodo = this.state.todo.filter(function (value, index){
            return value !== item;
        });

        this.setState({
            todo: newTodo
        })
    },

    addItem: function (item){
        let newTodo = this.state.todo;
        newTodo.push(item);

        this.setState({
            todo: newTodo
        });
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

// input component
var InputComponent = React.createClass({
    render: function (){
        return (
            <form id="formTag" onSubmit={this.submitHandler}>
                <input type="text" ref="inputTag" />
                <input type="submit" value="ok" />
            </form>
        );
    },

    submitHandler: function (event){
        event.preventDefault();
        this.props.whenSubmit(this.refs.inputTag.value);

    }
});

// put component into html page
ReactDOM.render(<TodoComponent />, document.querySelector(".header-title"));
```


jsx 테그에 ref 속성을 넣어주면 컴포넌트에서 this.refs로 ref가 적용된 dom을 가져올 수 있다. 리액트 도큐먼테이션에는 ref에 함수가 들어가는 코드로 만들어져 있던데, 함수로 사용하는 방법도 알아볼 필요가 있을 것 같다. 폼테그의 값을 가져오거나, 에니메이션을 줄 때 주로 사용한다.  


ref 속성은 컴포넌트가 mount되면 바로 실행된다. ref는 컴포넌트 속성으로 사용할 수도 있고, dom 엘리먼트에 사용할 수도 있다. dom 엘리먼트에 사용할 경우, 
dom 엘리먼트가 콜백함수의 첫번째 인자로 주어진다. dom 엘리먼트의 레퍼런스를 저장할 때 주로 사용한다고 한다. 

```javascript
<a href="#" className="listUnit-delete" data-index={index} onClick={this.deleteItem.bind(this, index)} ref={(button) => {this.button = button}}>삭제</a>
```
