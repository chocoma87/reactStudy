#Props
리액트 컴퍼넌트로 넘겨지는 데이터를 말한다.

###props 기본   
```
// create component
var TodoComponent = React.createClass({
    render: function(){
        return (
            <div>
                <h1>Hello</h1>
                <p>{this.props.day}</p>
            </div>
        );
    }
});

// put component into html page
ReactDOM.render(<TodoComponent day="목" />, document.querySelector(".header-title"));
```
여기서 this는 컴퍼넌트를 참조한다.


###props에 변수가 오는 경우   
```
// create component
var TodoComponent = React.createClass({
    render: function(){
        return (
            <div>
                <p><strong>Name</strong> {this.props.profile.name}</p>
                <p><strong>age</strong> {this.props.profile.age}</p>
                <p><strong>address</strong> {this.props.profile.address}</p>
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

이때 여러개의 props을 전달해 줄 수 있으며(day, profile), 변수를 prps으로 넘겨줄 때는 {val} 신텍스를 사용한다.
