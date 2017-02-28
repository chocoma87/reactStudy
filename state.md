#State
컴퍼넌트 안에서 지정해 준다. props와 비슷하지만, 해당 컴포넌트에서만 접할 수 있는 private 오브젝트이다. class로 생성된 컴포넌트만이 가지고 있는 기능으로 local state 이다. props을 사용할 건지, state를 사용할 것인지는 상황에 따라 결정한다.  

클래스가 아닌 컴포넌트의 예는 다음과 같다.

```
function TitleComponent (props){
    return (
        <div>{props.time}</div>
    )
}

ReactDOM.render(<TitleComponent time={new Date().toLocaleTimeString()} />, document.querySelector('.header-title'));
```


###state basic
```
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
컴포넌트에서 this로 접근할 수 있다.
