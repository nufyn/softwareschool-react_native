# 컴포넌트(Components)

컴포넌트를 통해 UI를 재사용 가능한 개별적인 여러 조각으로 나누고, 각 조각을 개별적으로 살펴볼 수 있습니다.

## 2 - 1) 컴포넌트란?

개념적으로 컴포넌트는 JAVASCRIPT 함수와 유사합니다. “props”라고 하는 임의의 입력을 받은 후, 화면에 어떻게 표시되는지를 기술하는 React 엘리먼트를 반환합니다.

<br/>

### 컴포넌트의 종류

1. functional 컴포넌트
2. class 컴포넌트

<br/>

### 컴포넌트의 정의

컴포넌트를 정의하는 가장 간단한 방법은 JAVASCRIPT 함수를 작성하는 것입니다.

#### 함수형 컴포넌트
```JAVASCRIPT
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}
```

이 함수는 데이터를 가진 하나의 “props” (props는 속성을 나타내는 데이터입니다) 객체 인자를 받은 후 React 엘리먼트를 반환하므로 유효한 React 컴포넌트입니다. 이러한 컴포넌트는 JAVASCRIPT 함수이기 때문에 말 그대로 “함수 컴포넌트”라고 호칭합니다.

그리고, ES6 class를 사용하여 컴포넌트를 정의할 수 있습니다.

#### 클래스 컴포넌트
```JAVASCRIPT
class Welcome extends React.Component {
  render() {
    return <h1>Hello, {this.props.name}</h1>;
  }
}
```

React의 관점에서 볼 때 위 두 가지 유형의 컴포넌트는 동일합니다.

클래스컴포넌트는 React에서 다양한 기능을 주기위해 만든 특수한 객체입니다.

_*과거 React에서는 class 컴포넌트의 역할이 중요했지만, 현재는 생김새외에 차이가 없습니다._

<br/>

### 컴포넌트 렌더링

React 엘리먼트는 사용자 정의 컴포넌트로도 나타낼 수 있습니다.

```JAVASCRIPT
const element = <Welcome name="Sara" />;
```

이때, React가 사용자 정의 컴포넌트로 작성한 엘리먼트를 발견하면 JSX 어트리뷰트와 자식을 해당 컴포넌트에 단일 객체로 전달합니다. 이 객체를 “props”라고 합니다.

```JAVASCRIPT
function Welcome(props) { 
  // 3. React DOM은 <h1>Hello, Sara</h1> 엘리먼트와 일치하도록 DOM을 효율적으로 업데이트합니다.
  return <h1>Hello, {props.name}</h1>; 
  // 4. Welcome 컴포넌트는 결과적으로 <h1>Hello, Sara</h1> 엘리먼트를 반환합니다.
}

const element = <Welcome name="Sara" />; // 2. {name: 'Sara'}를 props로 하여 Welcome 컴포넌트를 호출합니다.

ReactDOM.render(
  element,  // 1. 엘리먼트로 ReactDOM.render()를 호출합니다.
  document.getElementById('root')
);
```

_*컴포넌트를 명명할때, PascalCase를 사용합니다._


#### 컴포넌트의 활용
```JAVASCRIPT
function Welcome(props) {
  return <h1>Hello, {props.name}</h1>;
}

export default function App() {
  return (
    <div>
      <Welcome name="Sara" /> {/* <h1>Hello, Sara</h1> */}
      <Welcome name="Cahal" /> {/* <h1>Hello, Cahal</h1> */}
      <Welcome name="Edite" /> {/* <h1>Hello, Edite</h1> */}
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

![1](./4.jpg)

>일반적으로 새 React 앱은 최상위에 단일 App 컴포넌트를 가지고 있습니다. 하지만 기존 앱에 React를 통합하는 경우에는 Button과 같은 작은 컴포넌트부터 시작해서 뷰 계층의 상단으로 올라가면서 점진적으로 작업해야 할 수 있습니다.

<br/>

### 컴포넌트 요소 추출

프로젝트 중간중간 컴포넌트로 묶여있지만 구성요소마다 재사용을 또 해야할지도 모릅니다. 또, 컴포넌트내에 중첩된 요소와 중첩되지 말아야할 요소를 나뉘어야할 수 도 있습니다.

다른 웹사이트에서 코드 한 구절을 가져와 예시로 보겠습니다. 실행은 되지 않습니다.

```JAVASCRIPT
function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <img className="Avatar"
          src={props.author.avatarUrl}
          alt={props.author.name}
        />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

위 코드를 보면 작성자 아바타와 작성자 이름, 텍스트, 날짜가 포함된 컴포넌트가 있습니다.

추출 대상은 아바타와 작성자 이름이 적힌 author와 text, date정도 일 것 같습니다. 그럼 추출해보겠습니다.

#### Avatar 추출
```JAVASCRIPT
function Avatar(props) {
  return (
    // 아바타와 이름은 웹사이트 전역에서 사용가능한 데이터이니 user로 일반화를 시키겠습니다.
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}

function Comment(props) {
  return (
    <div className="Comment">
      <div className="UserInfo">
        <Avatar user={props.author} />
        <div className="UserInfo-name">
          {props.author.name}
        </div>
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

Comment라는 본체 컴포넌트가 좀 더 간결해 졌습니다. 하지만 그래도 뭔가 조금 아쉽습니다. 여러분들이 원하는 대로 구상하신 후, 컴포넌트를 추출해 자유롭게 구현해봅시다. 단, Comment는 가장 최상위 props를 받는 아주 단순한 형태의 컴포넌트가 되어야 합니다.

```JAVASCRIPT
function Avatar(props) {
  return (
    // 아바타와 이름은 웹사이트 전역에서 사용가능한 데이터이니 user로 일반화를 시키겠습니다.
    <img className="Avatar"
      src={props.user.avatarUrl}
      alt={props.user.name}
    />
  );
}

function UserInfo(props) {
  return (
    <>
      <Avatar user={props.user} />
      <div className="user-name">
        {props.user.name}
      </div>
    </>
  );
}


function Comment(props) {
  return (
    <div className="Comment">
      <div className="Comment-user">
        <UserInfo user={props.author} />
      </div>
      <div className="Comment-text">
        {props.text}
      </div>
      <div className="Comment-date">
        {formatDate(props.date)}
      </div>
    </div>
  );
}
```

>처음에는 컴포넌트를 추출하는 작업이 지루해 보일 수 있습니다. 하지만 재사용 가능한 컴포넌트를 만들어 놓는 것은 더 큰 앱에서 작업할 때 두각을 나타냅니다. UI 일부가 여러 번 사용되거나 (Button, Panel, Avatar), UI 일부가 자체적으로 복잡한 (App, FeedStory, Comment) 경우에는 별도의 컴포넌트로 만드는 게 좋습니다.

<br/>

### 주의할 점

모든 React 컴포넌트는 자신의 props를 다룰 때 반드시 순수 함수처럼 동작해야 합니다.

함수 컴포넌트나 클래스 컴포넌트 모두 컴포넌트의 자체 props를 수정해서는 안 됩니다. 다음 sum 함수를 살펴봅시다.

```JAVASCRIPT
function sum(a, b) {
  return a + b;
}
```

이런 함수들은 순수 함수라고 호칭합니다. 입력값을 바꾸려 하지 않고 항상 동일한 입력값에 대해 동일한 결과를 반환하기 때문입니다.

반면에 다음 함수는 자신의 입력값을 변경하기 때문에 순수 함수가 아닙니다.

```JAVASCRIPT
function withdraw(account, amount) {
  account.total -= amount;
}
```

***
