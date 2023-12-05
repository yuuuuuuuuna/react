
## hook이란
함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수
- 최상위(at the top level)에서만 Hook을 호출해야 한다.
- React 함수 컴포넌트 내에서만 Hook을 호출해야 한다.

### useState
```
import React, { useState } from 'react';

  function Example() {
    const [count, setCount] = useState(0);

    return (
      <div>
        <p>You clicked {count} times</p>
        <button onClick={() => setCount(count + 1)}>
         Click me
        </button>
      </div>
    );
  }
```
### useEffect
```
import React, { useState, useEffect } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  useEffect(() => {
    // 컴포넌트가 마운트될 때와 업데이트될 때 실행되는 코드
    document.title = `Count: ${count}`;

    // clean-up 함수 (컴포넌트가 언마운트되기 전에 실행)
    return () => {
      document.title = 'React App';
    };
  }, [count]); // count가 변경될 때만 useEffect 내부의 코드가 실행됨
}
```

### useContext
```
import React, { useContext } from 'react';
import MyContext from './MyContext';

function MyComponent() {
  const contextValue = useContext(MyContext);

  return <p>{contextValue}</p>;
}
```

### useReducer
```
import React, { useReducer } from 'react';

function reducer(state, action) {
  switch (action.type) {
    case 'increment':
      return { count: state.count + 1 };
    case 'decrement':
      return { count: state.count - 1 };
    default:
      return state;
  }
}

function MyComponent() {
  const [state, dispatch] = useReducer(reducer, { count: 0 });

  return (
    <div>
      <p>Count: {state.count}</p>
      <button onClick={() => dispatch({ type: 'increment' })}>Increment</button>
      <button onClick={() => dispatch({ type: 'decrement' })}>Decrement</button>
    </div>
  );
}
```

### useMemo
의존성 배열 안에있는 값이 업데이트 될 때에만 콜백 함수를 다시 호출하여 메모리에 저장된 값을 업데이트
```
import { useMemo, useEffect, useState } from "react";

function App() {
  const [number, setNumber] = useState(1);
  const [isKorea, setIsKorea] = useState(true);

  // 1번 location
  const location = {
    country: isKorea ? "한국" : "일본"
  };

  // 2번 location
  // const location = useMemo(() => {
  //   return {
  //     country: isKorea ? '한국' : '일본'
  //   }
  // }, [isKorea])

  useEffect(() => {
    console.log("useEffect 호출!");
  }, [location]);

  return (
    <header className="App-header">
      <h2>하루에 몇 끼 먹어요?</h2>
      <input
        type="number"
        value={number}
        onChange={(e) => setNumber(e.target.value)}
      />
      <hr />

      <h2>내가 있는 나라는?</h2>
      <p>나라: {location.country}</p>
      <button onClick={() => setIsKorea(!isKorea)}>Update</button>
    </header>
  );
}

export default App;
```

### useCallback
```
import React, { useState, useCallback } from 'react';

function MyComponent() {
  const [count, setCount] = useState(0);

  // 의존성 배열에 count를 추가하여 count가 변경될 때만 handleIncrement가 새로 생성됨
  const handleIncrement = useCallback(() => {
    setCount(count + 1);
  }, [count]);

  return (
    <div>
      <p>Count: {count}</p>
      <button onClick={handleIncrement}>Increment</button>
    </div>
  );
}
```

### useRef
```
import React, { useRef, useEffect } from 'react';

function MyComponent() {
  const myInputRef = useRef(null);

  useEffect(() => {
    // 컴포넌트가 마운트되면 input 요소에 포커스를 줌
    myInputRef.current.focus();
  }, []);

  return <input ref={myInputRef} />;
}
```
