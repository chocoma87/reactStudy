#Props
리액트 컴퍼넌트로 넘겨지는 데이터를 말한다.

###props 기본   
```javascript
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
여기서 this는 컴퍼넌트를 참조한다. props은 html 테그의 속성처럼 jsx 테그에 속성을 추가한다 라고 생각할 수 있다(syntex가 비슷함). 하지만 render 함수에서 불러오는 컴퍼넌트에서 해당 prop 값에 접근할 수 있다는게 차이점이라고 할 수 있다.

```
ReactDOM.render(<TodoComponent day={10} />, document.querySelector(".header-title"));
```
숫자를 넣을 때는 {}를 사용한다.  

###props에 변수가 오는 경우   
```javascript
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

이때 여러개의 props을 전달해 줄 수 있으며(day, profile), 변수를 prps으로 넘겨줄 때는 {val} 신텍스를 사용한다. 그리고 jsx에서 prop에 불러올 때에는 object이면 안된다. (array는 가능)


###props에 바로 스크립트 코드를 넣을 수 있다.
```javascript
var TitleComponent = React.createClass({
    render: function (){
        return (
            <div>
                <div>toay</div>
                <div>{this.props.time}</div>
            </div>
        )
    }
});

ReactDOM.render(<TitleComponent time={new Date().toLocaleTimeString()} />, document.querySelector('.header-title'));
```
하지만 여기서도 toLocaleTimeString로 date 오브젝트를 스트링으로 바꿔줬다. 


###child
props.children로 jsx 테그 안의 엘리먼트를 불러올 수 있다. 여러개의 child를 가질 수 있다.   
```javascript
// props.child는 Hello world! 스트링이 된다. 
<MyComponent>Hello world!</MyComponent>
```
