# react


### 1. JSX
JSX는 JavaScript의 확장 문법으로, XML과 유사한 구조
```
const root = ReactDOM.createRoot(document.getElementById('root'));
  
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  root.render(element);
}

setInterval(tick, 1000);
```

### 2. 컴포넌트(Component)
#### 클래스형 컴포넌트(Class Components)
- render 메서드를 포함, 이 메서드에서 컴포넌트의 UI를 반환.
- 상태(state)를 가질 수 있다.
- 라이프사이클 메서드를 활용할 수 있다.
```
import React, { Component } from 'react';

class MyComponent extends Component {
  render() {
    return <p>Hello, React!</p>;
  }
}

export default MyComponent;
```

#### 함수형 컴포넌트(Functional Components)
- useState 등의 훅을 사용하여 상태를 관리할 수 있다.
- 라이프사이클 메서드를 사용할 수 없지만, useEffect 훅을 통해 비슷한 작업을 수행할 수 있다.
```
import React from 'react';

function MyFunctionalComponent() {
  return <p>Hello, React!</p>;
}

export default MyFunctionalComponent;
```

### 3. 상태(State)와 속성(Props)
컴포넌트 내부에서 관리되는 데이터의 상태
```
import React, { useState } from 'react';

function MyFunctionalComponent() {
  // useState 훅을 사용하여 초기 상태를 설정
  const [count, setCount] = useState(0);
  const [text, setText] = useState('Hello, React!');

  return (
    <div>
      <p>{text}</p>
      <p>Count: {count}</p>
      <button onClick={() => setCount(count + 1)}>Increment</button>
    </div>
  );
}

export default MyFunctionalComponent;
```
- props는 (함수 매개변수처럼) 컴포넌트에 전달되는 반면 state는 (함수 내에 선언된 변수처럼) 컴포넌트 안에서 관리

### 4. 합성
상속 대신 합성 사용
```
function SplitPane(props) {
  return (
    <div className="SplitPane">
      <div className="SplitPane-left">
        {props.left}
      </div>
      <div className="SplitPane-right">
        {props.right}
      </div>
    </div>
  );
}

function App() {
  return (
    <SplitPane
      left={
        <Contacts />
      }
      right={
        <Chat />
      } />
  );
}
``
