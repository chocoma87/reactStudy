#JSX in React
jsx는 리액트 엘리먼트는 만들어 주는 javascript syntax extension 이다. 컴파일 된 후에는 일반적인 자바스크립트 오브젝트로 변환된다. 그래서 jsx에서 자바스크립트 코드를 실행 할 수도 있다.
보통 리액트와 함께 jsx를 사용하는데, jsx가 필수 사항은 아니다. jsx를 사용하지 않고, createElement함수로 리액트 엘리먼트를 만들어서 사용할 수도 있다. (실제로 babel이 컴파일 할때 jsx를 React.createElement로 변경한다. [onlnie bebel compiler](https://babeljs.io/repl/#?babili=false&evaluate=true&lineWrap=false&presets=es2015%2Creact%2Cstage-0&targets=&browsers=&builtIns=false&code=function%20hello()%20%7B%0A%20%20return%20%3Cdiv%3EHello%20world!%3C%2Fdiv%3E%3B%0A%7D))


createElement함수가 생성하는 오브젝트를 단순화해서 나타내면  아래와 같다.  
```javascript
// Note: this structure is simplified
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world'
  }
};
```

####주의
jsx안에서 for, if 같이 반환 값이 없는 코드는 사용 할 수  없다. 하지만 if나 for 안에 jsx가 들어가는 것은 가능하다.

```javascript
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```


##react element
리액트 엘리먼트란 리액트 어플리케이션에서 사용하는 최소단위의 블럭을 말한다. 화면에 무엇을 보여줄 것인지를 나타내는 것이다. 브라우저의 dom 엘리먼트와는 달리 리액트 엘리먼트는 아주 단순한(기능이 없는? 밋밋한?) 오브젝트이다. 그래서 생성하고 수정하는게 쉽고 빠르게 된다. 이러한 리액트 엘리먼트가 모여서 컴포넌트를  형성하게 된다.  
```javascript
const element = <h1>Hello, world</h1>;
```

##element without jsx
jsx를 사용하지 않고 리액트 엘리먼트를 만드는 방법은 아래와 
```javascript
React.createElement(
  type,
  [props],
  [...children]
)

// 활용 예  
const e = React.createElement;

ReactDOM.render(
  e('div', null, 'Hello World'),
  document.getElementById('root')
);
```

##element와 component의  차이  
컴포넌트는 ui를 작은 단위로 쪼갠 것으로 각각의 컴포넌트는 독립된 객체로  존재한다. 알기쉬운 예로 비교하자면, 자바스크립트의 함수와 비슷하다고 할 수 있다. input(리액트에서는 prop)을 받아서 리액트 엘리먼트를 반환해 준다. 
여기서 리액트 엘리먼트는 위에서 언급한 대로 화면에 무엇을 보여줄 것인지를 나타내는 블럭이다. 

컴포넌트의 간단한 예를 들면 다음과 같다. props를 받아서 화면에 h1테그로 출력해주는 리액트 엘리먼트를 반환해 주는걸 확인 할 수 있다.  
```javasript
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```













