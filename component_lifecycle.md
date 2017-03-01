###Component life cycle

리액트가 실행 될 때 함수가 실행되는 순서는 다음과 같다.  

1. getInitialState
2. componentWillMount
    - render 함수가 실행되기 전에 실행된다. dom 엘리먼트가 브라우져에 삽입되기 전 단계이다.
3. render 
    - dom 엘리먼트를 브라우져에 삽입하는 단계.
4. componentDidMount
    - 컴포넌트가 브라우져의 dom에 삽입 된 후에 실행된다.(함수가 정의되 있는 경우)
    - 데이터 베이스에서 데이터를 불러오기 좋은 단계이다.
    
    
    
    
###Updating life cycle
1. componentWillReceiveProps
    - pops를 받기 전에 실행된다.
    - 현재 props와 새로운 props를 비교해서 현재의 prop을 변경할때 사용할 수 있다.
2. shouldComponentUpdate
    - false를 받환시키면 업데이트가 되지 않는다. 이하 아래의 코드가 실행되지 않음. 
3. componentWillUpdate
4. render
5. componentDidUadate
    - dom 변환이 브라우져에 반영된 뒤에 실행된다. 이 단계에서 네트워크 요청을 할 수 있다. 
    
    
