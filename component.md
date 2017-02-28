#Component
리액트는 작은 컴포넌트의 조합으로 만들 수 있다. 컴포넌트 안에 컴퍼넌트가 있을 수도 있다. 

####여기서 컴퍼넌트란, 작은 조각으로 분리한 UI조각이라고 할 수 있는데, 서로 완전히 분리된 독립된 객체이며 따라서 재사용 할 수 있다.

###step1
리액트 오브젝트를 불러오면서 시작한다. 

```javascript
var React = require("react");
var ReactDOM = require("react-dom");
```

###step2
컴퍼넌트생성한다.  컴퍼넌트를 생성하는데는 2가지 방법이 있는데, es6를 사용하는 방법과 리액트 헬퍼메서드를 사용하는 방법이 있다. 
es6를 사용하는 방법은 classe를 사용하는 방법인데, 먼저 리액트 헬퍼 함수를 사용하는 방법으로 해보자. 

```
var TodoComponent = React.createClass({
    render: function(){
        return (
            <h1>Hello</h1>
        );
    }
});
```

##step2
생선한 컴퍼넌트를 html에 삽입한다. 

```javascript 
ReactDOM.render(<TodoComponent />, document.querySelector(".day"));
```


*ReactDOM 코드를 열어보니, 자바스크립트 객체로 트리구조의 가상 돔을 만들어서 사용하는 것 같다. 브라우저에서도 dom을 파싱할 때 트리구조로 만들어서 한다고 알고 있는데, 
가상 dom이라는게 html구조를 자바스크립트 객체로 표현한 것이었다.*
