# 1장. jsx 소개

## 1 - 1) jsx란

jsx는 html도 아닌것이 javascript도 아닌것 같은 문법입니다.
그 이유는 react에서 js를 직관적으로 보여주기 위해 html과 비슷한 xml로 확장시킨 문법이기 때문입니다.

아래 변수 선언을 살펴봅시다.
```JAVASCRIPT
const element = <h1>Hello, world!</h1>;
```

JSX는 기본적으로 이벤트가 처리되는 방식, 시간에 따라 state가 변하는 방식, 화면에 표시하기 위해 데이터가 준비되는 방식 등 렌더링 로직이 본질적으로 다른 UI 로직과 연결됩니다.

React는 별도의 파일에 마크업과 로직을 넣어 기술을 인위적으로 분리하는 대신, 둘 다 포함하는 “컴포넌트”라고 부르는 느슨하게 연결된 유닛으로 관심사를 분리합니다. 

React는 JSX 사용이 필수가 아니지만, 대부분의 사람은 JavaScript 코드 안에서 UI 관련 작업을 할 때 시각적으로 더 도움이 된다고 생각합니다. 또한 React가 더욱 도움이 되는 에러 및 경고 메시지를 표시할 수 있게 해줍니다.
<br/>

### JSX에 표현식 포함하기
아래 예시에서는 name이라는 변수를 선언한 후 중괄호로 감싸 JSX 안에 사용하였습니다.

```JAVASCRIPT
const name = 'Josh Perez';
const element = <h1>Hello, {name}</h1>;

ReactDOM.render(
  element,
  document.getElementById('root')
);
```
```JAVASCRIPT
function formatName(user) {
  return user.firstName + ' ' + user.lastName;
}

const user = {
  firstName: 'Harper',
  lastName: 'Perez'
};

const element = (
  <h1>
    Hello, {formatName(user)}!
  </h1>
);

ReactDOM.render(
  element,
  document.getElementById('root')
);
```

가독성을 좋게 하기 위해 JSX를 여러 줄로 나눴습니다. 필수는 아니지만, 이 작업을 수행할 때 자동 세미콜론 삽입을 피하고자 괄호로 묶는 것을 권장합니다.

<br/>

### JSX도 표현식입니다
컴파일이 끝나면, JSX 표현식이 정규 JavaScript 함수 호출이 되고 JavaScript 객체로 인식됩니다.

즉, JSX를 if 구문 및 for loop 안에 사용하고, 변수에 할당하고, 인자로서 받아들이고, 함수로부터 반환할 수 있습니다.
```JAVASCRIPT
function getGreeting(user) {
  if (user) {
    return <h1>Hello, {formatName(user)}!</h1>;
  }
  return <h1>Hello, Stranger.</h1>;
}
```

<br/>

### JSX 속성 정의
속성에 따옴표를 이용해 문자열 리터럴을 정의할 수 있습니다.
```JAVASCRIPT
const element = <div tabIndex="0"></div>;
```
중괄호를 사용하여 어트리뷰트에 JavaScript 표현식을 삽입할 수도 있습니다.

```JAVASCRIPT
const element = <img src={user.avatarUrl}></img>;
```

어트리뷰트에 JavaScript 표현식을 삽입할 때 중괄호 주변에 따옴표를 입력하지 마세요. 따옴표(문자열 값에 사용) 또는 중괄호(표현식에 사용) 중 하나만 사용하고, 동일한 어트리뷰트에 두 가지를 동시에 사용하면 안 됩니다.

_*JSX는 HTML보다는 JavaScript에 가깝기 때문에, React DOM은 HTML 어트리뷰트 이름 대신 camelCase 프로퍼티 명명 규칙을 사용합니다._

<br/>

### JSX로 자식 정의
태그가 비어있다면 XML처럼 /> 를 이용해 바로 닫아주어야 합니다.
```JAVASCRIPT
const element = <img src={user.avatarUrl} />;
```

JSX 태그는 자식을 포함할 수 있습니다.

```JAVASCRIPT
const element = (
  <div>
    <h1>Hello!</h1>
    <h2>Good to see you here.</h2>
  </div>
);
```

_*JSX는 주입 공격을 방지합니다. JSX에 사용자 입력을 삽입하는 것은 안전합니다._

```JAVASCRIPT
const title = response.potentiallyMaliciousInput;
// 이것은 안전합니다.
const element = <h1>{title}</h1>;
```

기본적으로 React DOM은 JSX에 삽입된 모든 값을 렌더링하기 전에 이스케이프 하므로, 애플리케이션에서 명시적으로 작성되지 않은 내용은 주입되지 않습니다. 모든 항목은 렌더링 되기 전에 문자열로 변환됩니다. 이런 특성으로 인해 XSS (cross-site-scripting) 공격을 방지할 수 있습니다.

<br/>

### JSX는 객체를 표현합니다.
Babel은 JSX를 React.createElement() 호출로 컴파일합니다.

다음 두 예시는 동일합니다.

```JAVASCRIPT
const element = (
  <h1 className="greeting">
    Hello, world!
  </h1>
);
const element = React.createElement(
  'h1',
  {className: 'greeting'},
  'Hello, world!'
);
```

React.createElement()는 버그가 없는 코드를 작성하는 데 도움이 되도록 몇 가지 검사를 수행하며, 기본적으로 다음과 같은 객체를 생성합니다.

```JAVASCRIPT
// 주의: 다음 구조는 단순화되었습니다
const element = {
  type: 'h1',
  props: {
    className: 'greeting',
    children: 'Hello, world!'
  }
};
```

이러한 객체를 “React 엘리먼트”라고 하며, 이를 화면에 표시하려는 항목에 대한 설명이라고 생각할 수 있습니다. React는 이러한 객체를 읽은 후 DOM을 구성하고 최신으로 유지하는 데 이러한 객체를 사용합니다.s

<br/>

### JSX 없이 사용하는 React
React를 사용할 때 JSX는 필수가 아닙니다. 빌드 환경에서 컴파일 설정을 하고 싶지 않을 때 JSX 없이 React를 사용하는 것은 특히 편리합니다.

각 JSX 엘리먼트는 React.createElement(component, props, ...children)를 호출하기 위한 문법 설탕입니다. 그래서 JSX로 할 수 있는 모든 것은 순수 JavaScript로도 할 수 있습니다.

예를 들어 다음의 JSX로 작성된 코드는
```JAVASCRIPT
class Hello extends React.Component {
  render() {
    return <div>Hello {this.props.toWhat}</div>;
  }
}

ReactDOM.render(
  <Hello toWhat="World" />,
  document.getElementById('root')
);
```
아래처럼 JSX를 사용하지 않은 코드로 컴파일될 수 있습니다.
```JAVASCRIPT
class Hello extends React.Component {
  render() {
    return React.createElement('div', null, `Hello ${this.props.toWhat}`);
  }
}

ReactDOM.render(
  React.createElement(Hello, {toWhat: 'World'}, null),
  document.getElementById('root')
);
```

컴포넌트는 문자열이나 React.Component의 하위 클래스 또는 컴포넌트를 위한 일반 함수로 제공됩니다.
React.createElement를 너무 많이 입력하는 것이 피곤하다면 짧은 변수에 할당하는 방법이 있습니다.

```JAVASCRIPT
const e = React.createElement;

ReactDOM.render(
  e('div', null, 'Hello World'),
  document.getElementById('root')
);
```
React.createElement를 짧은 변수에 할당하면 편리하게 JSX 없이 React를 사용할 수 있습니다.

#### jsx Fragment

부모 자식 컴포넌트 사이에 기존의 html모습과 맞지않는 형태가 생겨날 수 있습니다.

```JAVASCRIPT
class Columns extends React.Component {
  render() {
    return (
      // jsx규칙에 의해 삽입된 필요없는 태그
      <div> 
        <td>Hello</td>
        <td>World</td>
      </div>
    );
  }
}
class Table extends React.Component {
  render() {
    return (
      <table>
        <tr>
          <Columns />
        </tr>
      </table>
    );
  }
}
// 이러면 table 사이에 필요없는 div가 들어가게 됩니다.
```

그럴때 사용하는 것이 Fragment입니다.

```JAVASCRIPT
class Columns extends React.Component {
  render() {
    return (
      //jsx규칙을 지키기위해 만들어진 Fragment는 아무의미가 없는 태그입니다. <> </> 
      <React.Fragment> 
        <td>Hello</td>
        <td>World</td>
      </React.Fragment>
    );
  }
}
class Table extends React.Component {
  render() {
    return (
      <table>
        <tr>
          <Columns />
        </tr>
      </table>
    );
  }
}
// 이러면 <tr>태그 밑에 바로 <td>가 옵니다
```

<br/>

## 1 - 2) element

엘리먼트는 react에서 가장 작은 단위입니다.

```JAVASCRIPT
const element = <h1>Hello, world</h1>;
```

브라우저 DOM 엘리먼트와 달리 React 엘리먼트는 일반 객체이며(plain object) 쉽게 생성할 수 있습니다.

#### 엘리먼트 렌더링
```JAVASCRIPT
<div id="root"></div>

const element = <h1>Hello, world</h1>;
ReactDOM.render(element, document.getElementById('root'));
```

React 엘리먼트는 불변객체입니다. 한번 렌더링된 엘리먼트는 실제로는 업데이트 되지 않습니다. 그렇다면 react는 어떻게 페이지를 업데이트 할까요?

#### 엘리먼트 업데이트
```JAVASCRIPT 
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(element, document.getElementById('root'));
}

setInterval(tick, 1000);
```

![tick](../../제목없음.png)

엘리먼트는 영화에서 하나의 프레임과 같이 특정 시점의 UI를 보여줍니다. 즉, React DOM은 해당 엘리먼트와 그 자식 엘리먼트를 이전의 엘리먼트와 비교하고 DOM을 원하는 상태로 만드는데 필요한 경우에만 DOM을 업데이트합니다.

_*여기서 주의할 점이 있습니다.
components 와 element를 혼동하지 맙시다. 엘리먼트는 컴포넌트의 “구성 요소”입니다.
다음장에서 컴포넌트에 대해서 알아봅시다._

***
