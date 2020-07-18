# 핵심 핸들링 기능

## 4 - 1) react에서 event 처리

event처리에 관한 지식은 html과 자바스크립트에서 충분히 학습하셨으리라 생각됩니다. React에서의 event처리도 기존의 DOM 엘리먼트에서 이벤트를 처리하는 방식과 매우 유사합니다. 하지만 몇 가지 문법에 차이는 있습니다.

### React event처리의 특징

- React의 이벤트는 소문자 대신 캐멀 케이스(camelCase)를 사용합니다.
- JSX를 사용하여 문자열이 아닌 함수로 이벤트 핸들러를 전달합니다.

```html
<button onclick="activateLasers()">
  Activate Lasers
</button>
```

```javascript
<button onClick={activateLasers}>
  Activate Lasers
</button>
```

또 다른 차이점으로, React에서는 false를 반환해도 기본 동작을 방지할 수 없습니다. 반드시 preventDefault를 명시적으로 호출해야 합니다. 예를 들어, 일반 HTML에서는 새 페이지를 여는 링크의 기본 동작을 방지하기 위해 다음과 같은 코드를 작성합니다.

```html
<a href="#" onclick="console.log('The link was clicked.'); return false">
  Click me
</a>
```

```javascript
 function handleClick(e) {
    e.preventDefault();
    console.log('The link was clicked.');
  }

  return (
    <a href="#" onClick={handleClick}>
      Click me
    </a>
```

_*여기서 e는 합성이벤트입니다._

React를 사용할 때 DOM 엘리먼트가 생성된 후 리스너를 추가하기 위해 addEventListener를 호출할 필요가 없습니다. 대신, 엘리먼트가 처음 렌더링될 때 리스너를 제공하면 됩니다.

클래스 콤포넌트에서 보통은 이벤트 핸들러를 클래스의 메서드로 만듭니다. 예를 들어, 다음 Toggle 컴포넌트는 사용자가 “ON”과 “OFF” 상태를 토글 할 수 있는 버튼을 렌더링합니다.

```javascript
class Toggle extends React.Component {
  constructor(props) {
    super(props);
    this.state = {isToggleOn: true};

    // 콜백에서 `this`가 작동하려면 아래와 같이 바인딩 해주어야 합니다.
    this.handleClick = this.handleClick.bind(this);
  }

  handleClick() {
    this.setState(state => ({
      isToggleOn: !state.isToggleOn
    }));
  }

  render() {
    return (
      <button onClick={this.handleClick}>
        {this.state.isToggleOn ? 'ON' : 'OFF'}
      </button>
    );
  }
}

ReactDOM.render(
  <Toggle />,
  document.getElementById('root')
);
```

## 4 - 2) 조건부 렌더링

React에서는 원하는 동작을 캡슐화하는 컴포넌트를 만들 수 있습니다. 이렇게 하면 애플리케이션의 상태에 따라서 컴포넌트 중 몇 개만을 렌더링할 수 있습니다.

React에서 조건부 렌더링은 JavaScript에서의 조건 처리와 같이 동작하기 때문에 __if__ 나 __조건부 연산자(삼항 조건 연산자)__ 와 같은 JavaScript 연산자를 현재 상태를 나타내는 엘리먼트를 만드는 데에 사용하세요. 그러면 React는 현재 상태에 맞게 UI를 업데이트할 것입니다.

#### 조건에 따라 콤포넌트를 다르게 렌더링
```javascript
function UserGreeting(props) {
  return <h1>Welcome back!</h1>;
}

function GuestGreeting(props) {
  return <h1>Please sign up.</h1>;
}

function Login(props) {
  const isLoggedIn = props.isLoggedIn;
  if (isLoggedIn) {
    return <UserGreeting />;
  }
  return <GuestGreeting />;
}

ReactDOM.render(
  // Try changing to isLoggedIn={true}:
  <Login isLoggedIn={false} />,
  document.getElementById('root')
);
```

이렇게 조건부 렌더링을 테스트해보았습니다. 로그인상태에 따라 다른 ui를 렌더링합니다.

#### 심화
```javascript
class Login extends React.Component {
  constructor(props) {
    super(props);
    this.handleLoginClick = this.handleLoginClick.bind(this);
    this.handleLogoutClick = this.handleLogoutClick.bind(this);
    this.state = {isLoggedIn: false};
  }

  handleLoginClick() {
    this.setState({isLoggedIn: true});
  }

  handleLogoutClick() {
    this.setState({isLoggedIn: false});
  }

  render() {
    const isLoggedIn = this.state.isLoggedIn;
    let button;
    if (isLoggedIn) {
      button = <LogoutButton onClick={this.handleLogoutClick} />;
    } else {
      button = <LoginButton onClick={this.handleLoginClick} />;
    }

    return (
      <div>
        <Greeting isLoggedIn={isLoggedIn} />
        {button}
      </div>
    );
  }
}

ReactDOM.render(
  <Login />,
  document.getElementById('root')
);
```

## 4 - 3) map과 key

### map

javascript와 react에서는 어떻게 쓰이는 지 먼저 보겠습니다.
아래는 map()함수를 이용하여 numbers 배열의 값을 두배로 만든 후 map()에서 반환하는 새 배열을 doubled 변수에 할당하고 로그를 확인하는 코드입니다.

#### javascript
```JAVASCRIPT
const numbers = [1, 2, 3, 4, 5];
const doubled = numbers.map((number) => number);
console.log(doubled);
```

#### react
```JAVASCRIPT
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li>{number}</li>
);

ReactDOM.render(
  <ul>{listItems}</ul>,
  document.getElementById('root')
);
```

보통은 콤포넌트 하나로 묶어서 사용합니다.

#### react
```JAVASCRIPT
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li>{number}</li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);

```

코드를 이렇게 작성하였다면, 아마 에러내지 경고문구가 떴을겁니다. 경고문구는 리스트의 각 항목에 key를 넣어야 한다고 말합니다. “key”는 엘리먼트 리스트를 만들 때 포함해야 하는 특수한 문자열 atribute입니다. 다음 섹션에서 key의 중요성에 대해서 더 설명하겠습니다. 

일단은 numbers.map() 안에서 리스트의 각 항목에 key를 할당하여 키 누락 문제를 해결하겠습니다.

#### key 할당
```JAVASCRIPT
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <li key={number.toString()}>
      {number}
    </li>
  );
  return (
    <ul>{listItems}</ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

### key

Key는 React가 어떤 항목을 변경, 추가 또는 삭제할지 식별하는 것을 돕습니다. key는 엘리먼트에 안정적인 고유성을 부여하기 위해 배열 내부의 엘리먼트에 지정해야 합니다.

#### 일반적인 경우
```JAVASCRIPT
const numbers = [1, 2, 3, 4, 5];
const listItems = numbers.map((number) =>
  <li key={number.toString()}>
    {number}
  </li>
);
```

#### 객체 데이터를 받을 경우
```JAVASCRIPT
const todoItems = todos.map((todo) =>
  <li key={todo.id}>
    {todo.text}
  </li>
);
```

_*렌더링 한 항목에 대한 안정적인 ID가 없다면 최후의 수단으로 항목의 인덱스를 key로 사용할 수 있습니다. 하지만 권장하지는 않습니다._

### 키는 주변 배열의 context에서만 의미가 있습니다.

예를 들어 ListItem 컴포넌트를 추출 한 경우 ListItem 안에 있는 li 엘리먼트가 아니라 배열의 ListItem 엘리먼트가 key를 가져야 합니다.

#### 예시
```JAVASCRIPT
function ListItem(props) {
  const value = props.value;
  return (
    // 틀렸습니다! 여기에는 key를 지정할 필요가 없습니다.
    <li key={value.toString()}>
    {/*<li>*/}
      {value}
    </li>
  );
}

function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    // 맞습니다! 배열 안에 key를 지정해야 합니다.
    <ListItem key={number.toString()} value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}

const numbers = [1, 2, 3, 4, 5];
ReactDOM.render(
  <NumberList numbers={numbers} />,
  document.getElementById('root')
);
```

_*경험상 map() 함수 내부에 있는 엘리먼트에 key를 넣어 주는 게 좋습니다._

### Key는 형제 사이에서만 고유한 값이어야 한다.

Key는 배열 안에서 형제 사이에서 고유해야 하고 전체 범위에서 고유할 필요는 없습니다. 두 개의 다른 배열을 만들 때 동일한 key를 사용할 수 있습니다.

#### 예시
```JAVASCRIPT
function Blog(props) {
  const sidebar = (
    <ul>
      {props.posts.map((post) =>
        <li key={post.id}>
          {post.title}
        </li>
      )}
    </ul>
  );
  const content = props.posts.map((post) =>
    <div key={post.id}>
      <h3>{post.title}</h3>
      <p>{post.content}</p>
    </div>
  );
  return (
    <div>
      {sidebar}
      <hr />
      {content}
    </div>
  );
}

const posts = [
  {id: 1, title: 'Hello World', content: 'Welcome to learning React!'},
  {id: 2, title: 'Installation', content: 'You can install React from npm.'}
];
ReactDOM.render(
  <Blog posts={posts} />,
  document.getElementById('root')
);
```

### key는 힌트를 제공하지만 컴포넌트로 전달하지는 않습니다.

마지막으로, React에서 key는 힌트를 제공하지만 컴포넌트로 전달하지는 않습니다. 컴포넌트에서 key와 동일한 값이 필요하면 다른 이름의 prop으로 명시적으로 전달합니다.

#### 예시
```JAVASCRIPT
const content = posts.map((post) =>
  <Post
    key={post.id}
    id={post.id}
    title={post.title} />
);
```

### JSX에 map() 포함시키기

```JAVASCRIPT
function NumberList(props) {
  const numbers = props.numbers;
  const listItems = numbers.map((number) =>
    <ListItem key={number.toString()}
              value={number} />
  );
  return (
    <ul>
      {listItems}
    </ul>
  );
}
```

JSX를 사용하면 중괄호 안에 모든 표현식을 포함 시킬 수 있으므로 map() 함수의 결과를 인라인으로 처리할 수 있습니다.

```JAVASCRIPT
function NumberList(props) {
  const numbers = props.numbers;
  return (
    <ul>
      {numbers.map((number) =>
        <ListItem key={number.toString()}
                  value={number} />
      )}
    </ul>
  );
}
```

> 이 방식을 사용하면 코드가 더 깔끔해 지지만, 이 방식을 남발하는 것은 좋지 않습니다. JavaScript와 마찬가지로 가독성을 위해 변수로 추출해야 할지 아니면 인라인으로 넣을지는 개발자가 직접 판단해야 합니다. map() 함수가 너무 중첩된다면 컴포넌트로 추출 하는 것이 좋습니다.

***
