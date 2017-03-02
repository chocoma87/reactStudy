#Component
리액트는 작은 컴포넌트의 조합으로 만들 수 있다. 컴포넌트 안에 컴퍼넌트가 있을 수도 있다. 

####여기서 컴퍼넌트란, 작은 조각으로 분리한 UI조각이라고 할 수 있는데, 서로 완전히 분리된 독립된 객체이며 따라서 재사용 할 수 있다.

###basic use
```javascript
ReactDOM.render(<h1>hello</h1>, document.querySelector(".header-title"));
```
React.createClass 없이 jsx 테그를 바로 render할 수 있다.


###step1
리액트 오브젝트를 불러오면서 시작한다. 

```javascript
var React = require("react");
var ReactDOM = require("react-dom");
```

###step2
컴퍼넌트생성한다.  컴퍼넌트를 생성하는데는 2가지 방법이 있는데, es6를 사용하는 방법과 리액트 헬퍼메서드를 사용하는 방법이 있다. 
es6를 사용하는 방법은 classe를 사용하는 방법인데, 먼저 리액트 헬퍼 함수를 사용하는 방법으로 해보자. 

```javascript
// 꼭 대문자로
var TodoComponent = React.createClass({
    render: function(){
        return (
            <h1>Hello</h1>
        );
    }
});
```

createClass 함수는 오브젝트를 인자로 받는다. 오브젝트에는 여러개의 메서드가 올 수 있는데, 그중 하나가 render 메서드이다. render 메서드가 리턴해 주는 값은 JSX인데, 나중에 html로 변환되서 html 파일에 삽입되는 코드로 document.createElement와 비슷한 역할을 한다고 생각하면 된다. 

그리고 주의할 점은 아래와 같은 코드는 동작하지 않는다.

```javascript
var TodoComponent = React.createClass({
    render: function(){
        return (
            <h1>Hello</h1>
            <p>Gool morning</p>
        );
    }
});
```
top level 테그는 하나만 존재해야 하기 때문이다. 위와 같은 구조를 만들고 싶다면 아래와 같이 수정하면 동작한다. 


```javascript
var TodoComponent = React.createClass({
    render: function(){
        return (
            <div>
                <h1>Hello</h1>
                <p>Gool morning</p>
            </div>
        );
    }
});
```
그리고 또한가지, 변수명은 반드시 대문자로 시작해야 한다.소문자로 할 경우, 클래스가 아닌 평범한 html 테그로 인식하기 때문에 반드시 첫문자는 대문자로써야 한다.아래 코드를 보면 이해가 쉬움. 그리고 테그 사이에 바로 javascript 코드를 넣을 수는 없다.(스트링으로 코드가 그대로 출력됨.)

##step3
생선한 컴퍼넌트를 html에 삽입한다. 

```javascript 
ReactDOM.render(<TodoComponent />, document.querySelector(".day"));
ReactDOM.render(<삽입할 컴퍼넌트 이름 />, 컴퍼넌트가 삽입될 html);
```



#####ReactDOM 코드를 열어보니, 자바스크립트 객체로 트리구조의 가상 돔을 만들어서 사용하는 것 같다. 브라우저에서도 dom을 파싱할 때 트리구조로 만들어서 한다고 알고 있는데, 가상 dom이라는게 html구조를 자바스크립트 객체로 표현한 것이었다.

###React Developer Tool
[React Developer Tool](https://chrome.google.com/webstore/detail/react-developer-tools/fmkadmapgofadopljbjfkapdkoienihi/related?hl=en)라는 리액트 디버깅 툴이 있다. 설치하고 나면 크롬 개발자 도구에 react라는 탭이 생기는데 컴포넌트정보 등을 볼 수 있다. BBC, air bnb 처럼 리액트로 만든 사이트에 들어가서 개발자 도구로 살펴보는 것도 도움이 될 것 같다.
