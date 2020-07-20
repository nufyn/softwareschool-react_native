# react hooks

Hook이 React 버전 16.8에 새로 추가되었습니다. 

## 1) Hook의 개요


Hook을 이용하여 Class를 작성할 필요 없이 상태 값과 여러 React의 기능을 사용할 수 있습니다.

Hook은 함수 컴포넌트에서 React state와 생명주기 기능(lifecycle features)을 “연동(hook into)“할 수 있게 해주는 함수입니다. Hook은 class 안에서는 동작하지 않습니다. 대신 class 없이 React를 사용할 수 있게 해주는 것입니다.

<br/>

#### hook의 형태
```javascript
import React, { useState } from 'react';

export default function Example() {
  // "count"라는 새로운 상태 값을 정의합니다.
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

![1](./2.jpg)

>주의
React 16.8.0은 Hook를 지원하는 첫 번째 배포입니다. 업그레이드 할 때 React DOM을 포함한 모든 패키지를 업데이트 하는 것을 잊지 마세요. React Native는 v0.59부터 Hook을 지원합니다.

<br/>

### Hook 이전의 문제점

1. 복잡한 컴포넌트들은 이해하기 어렵습니다.
2. Class 콤포넌트는 사람과 기계를 혼동시킵니다.
3. 컴포넌트 사이에서 상태와 관련된 로직을 재사용하기 어렵습니다.

<br/>

### Hook의 특징

1. 선택적 사용 기존의 코드를 다시 작성할 필요 없이 일부의 컴포넌트들 안에서 Hook를 사용할 수 있습니다. 그러나 만약 당장 Hook이 필요 없다면, Hook를 사용할 필요는 없습니다.
2. 100% 이전 버전과의 호환성 Hook는 호환성을 깨뜨리는 변화가 없습니다.
3. 현재 사용 가능 Hook는 배포 v16.8.0에서 사용할 수 있습니다.
4. Hook는 props, state, context, refs, 그리고 lifecycle와 같은 React 개념에 좀 더 직관적인 API를 제공합니다.
5. Hook는 계층 변화 없이 상태 관련 로직을 재사용할 수 있도록 도와줍니다.
6. Hook은 class콤포넌트에서는 동작하지 않습니다. 함수형콤포넌트를 위해 고안된 개념입니다.

<br/>

### Hook의 종류

1. State Hook
2. Effect Hook
3. Custum Hook

<br/>

## 2) State Hook

기존에는 함수형 콤포넌트에서 state를 사용할 수 없었지만, Hook을 호출해 state를 추가할 수 있습니다. 

<br/>

#### useState가 Hook입니다. 
```javascript
import React, { useState } from 'react';

export default function Example() {
  // "count"라는 새 상태 변수를 선언합니다
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

_*기본적으로 react에 내장된 state와 이번에 새롭게 추가된 useState는 다릅니다._

#### class 콤포넌트의 경우
```javascript
export default class Example extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      count: 0
    };
  }

  render() {
    return (
      <div>
        <p>You clicked {this.state.count} times</p>
        <button onClick={() => this.setState({ count: this.state.count + 1 })}>
          Click me
        </button>
      </div>
    );
  }
}
```

useState는 현재의 state 값과 이 값을 업데이트하는 함수를 쌍으로 제공합니다. 
useState는 인자로 초기 state 값을 하나 받습니다. 카운터는 0부터 시작하기 때문에 위 예시에서는 초기값으로 0을 넣어준 것입니다.

#### 물론, 하나의 콤포넌트내에서 여러개의 state 를 사용할 수도 있습니다.
```javascript
function ExampleWithManyStates() {
  // 상태 변수를 여러 개 선언했습니다!
  const [age, setAge] = useState(42);
  const [fruit, setFruit] = useState('banana');
  const [todos, setTodos] = useState([{ text: 'Learn Hooks' }]);
  // ...
}
```

<br/>

## 3) Effect Hook

React 컴포넌트 안에서 데이터를 가져오거나 구독하고, DOM을 직접 조작하는 작업을 “side effects”(또는 짧게 “effects”)라고 합니다. 왜냐하면 이것은 다른 컴포넌트에 영향을 줄 수도 있고, 렌더링 과정에서는 구현할 수 없는 작업이기 때문입니다.

Effect Hook, 즉 useEffect는 함수 컴포넌트 내에서 이런 side effects를 수행할 수 있게 해줍니다. 

React class의 componentDidMount 나 componentDidUpdate, componentWillUnmount와 같은 목적으로 제공되지만, 하나의 API로 통합된 것입니다.

#### useEffect도 Hook입니다.
```javascript
import React, { useState, useEffect } from 'react';

export default function Example() {
  const [count, setCount] = useState(0);

  // componentDidMount, componentDidUpdate와 비슷합니다
  useEffect(() => {
    // 브라우저 API를 이용해 문서의 타이틀을 업데이트합니다
    document.title = `You clicked ${count} times`;
  });

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

useEffect를 사용하면, React는 DOM을 바꾼 뒤에 “effect” 함수를 실행할 것입니다. Effects는 컴포넌트 안에 선언되어있기 때문에 props와 state에 접근할 수 있습니다. 

>기본적으로 React는 매 렌더링 이후에 effects를 실행합니다. 첫 번째 렌더링도 포함해서요.

Effect를 “해제”할 필요가 있다면, 해제하는 함수를 반환해주면 됩니다. 이는 선택적입니다(optional). 예를 들어, 이 컴포넌트는 친구의 접속 상태를 구독하는 effect를 사용했고, 구독을 해지함으로써 해제해줍니다.

#### Effect 해제
```javascript
import React, { useState, useEffect } from 'react';

export default function FriendStatus(props) {
  const [isOnline, setIsOnline] = useState(null);

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}
```

#### usestate와 마찬가지로 하나의 콤포넌트 안에 여러개의 effect가능
```javascript
import React, { useState, useEffect } from 'react';

export default function FriendStatusWithCounter(props) {
  const [count, setCount] = useState(0);
  useEffect(() => {
    document.title = `You clicked ${count} times`;
  });

  const [isOnline, setIsOnline] = useState(null);
  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  function handleStatusChange(status) {
    setIsOnline(status.isOnline);
  }

  useEffect(() => {
    ChatAPI.subscribeToFriendStatus(props.friend.id, handleStatusChange);
    return () => {
      ChatAPI.unsubscribeFromFriendStatus(props.friend.id, handleStatusChange);
    };
  });

  if (isOnline === null) {
    return 'Loading...';
  }
  return isOnline ? 'Online' : 'Offline';
}

```

## 4) Hook 사용 규칙

1. 최상위(at the top level)에서만 Hook을 호출해야 합니다. 
2. 반복문, 조건문, 중첩된 함수 내에서 Hook을 실행하지 마세요.
3. React 함수 컴포넌트 내에서만 Hook을 호출해야 합니다. 일반 JavaScript 함수에서는 Hook을 호출해서는 안 됩니다. 

***
