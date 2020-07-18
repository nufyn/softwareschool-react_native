# 핵심 개념

## 3 - 1) State

__State는 props와 유사하지만__, 컴포넌트에 의해 완전히 제어됩니다.

이전에 예시로 사용했던 엘리먼트렌더링 코드는 하나의 virtual dom의 동작 방법을 알아보기 위한 것이었습니다.

#### 엘리먼트 렌더링
```javascript
function tick() {
  const element = (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {new Date().toLocaleTimeString()}.</h2>
    </div>
  );
  ReactDOM.render(
    element,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

이제 우리는 저 1초 단위 시계 코드를 캡슐화하고 자체 동작이 가능한 컴포넌트로 만들어 재사용하는 것을 해볼 것입니다.

#### 콤포넌트 렌더링
```JAVASCRIPT
function Clock(props) {
  return (
    <div>
      <h1>Hello, world!</h1>
      <h2>It is {props.date.toLocaleTimeString()}.</h2>
    </div>
  );
}

function tick() {
  ReactDOM.render(
    <Clock date={new Date()} />,
    document.getElementById('root')
  );
}

setInterval(tick, 1000);
```

일단 엘리먼트를 콤포넌트 안에 넣어서 콤포넌트를 렌더링하는 것으로 캡슐화 했습니다.

DOM을 구성하는 내용을 담은 콤포넌트인 함수와 콤포넌트를 렌더링하는 두 개의 함수로 1초마다 virtualDOM을 새롭게 받아 DOM을 업데이트하는 코드를 만들었습니다. 하지만 저희가 원하는 모습은 아래의 형태입니다.

#### 이상적인 형태
```JAVASCRIPT
function Clock() {
  return (
        // ...
        // 어떻게 해야 할까요?
  );
}

function App() {
  return (
    <React.Fragment>
      <Clock />
      <Clock />
      <Clock />
    </React.Fragment>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

여기서 우리는 두가지를 고민해야 합니다.

1. 콤포넌트가 자체적으로 UI를 가지고 있어야 한다.
2. 콤포넌트가 자체적으로 UI를 업데이트해야 한다.

어떻게 해야 할까요?

일단, 저희는 지금 클래스콤포넌트와 함수형 콤포넌트의 차이를 잘 알고 있습니다. 현재 우리의 지식과 위의 코드 구상에선 함수형 콤포넌트로는 이상적인형태를 만들 수 없음을 알아야 합니다. 이제부터 우리는 __State__ 라는 것을 활용하여 콤포넌트에 생명력을 불어넣음과 동시에 클래스콤포넌트의 내부를 꼼꼼히 살펴보겠습니다.

_*지금은 클래스콤포넌트로 작성합니다. 후에 함수형 콤포넌트로 전환하도록 합니다._

#### 클래스 콤포넌트
```JAVASCRIPT
// 함수형 콤포넌트를 확장하기 위해 react에 내장된 es6문법을 사용하여 class로 전환합니다.
class Clock extends React.Component {
  // render()라고 불리는 빈 메서드를 추가합니다. 클래스 콤포넌트를 작성할때 기본이 되는 틀입니다.
  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        {/*클래스안으로 들어온 props들은 this 키워드를 사용합니다.*/}
        <h2>It is {this.props.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

이제 과거의 함수형 콤포넌트는 클래스 콤포넌트로 전환되었습니다. 그러면서 __render__ 메서드를 갖게 되었는데, render 메서드는 업데이트가 발생할 때마다 호출되지만, 같은 DOM 노드로 <Clock />을 렌더링하는 경우 Clock 클래스의 단일 인스턴스만 사용됩니다. 이것은 로컬 state와 lyfecycle 메서드와 같은 부가적인 기능을 사용할 수 있게 해줍니다.

자, 그럼 state를 사용해 보겠습니다.

#### state 추가
```JAVASCRIPT
class Clock extends React.Component {
  // 새 constructor를 만들어 초기 state를 설정해 봅시다.
  constructor(props) { // 클래스 컴포넌트는 항상 props로 기본 constructor를 호출해야 합니다.
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2> {/*props를 state로 지정하여 콤포넌트내에서 제어할 수 있도록 합니다.*/}
      </div>
    );
  }
}
```

저기까지 되었다면, renderDOM의 엘리먼트에는 date props가 필요없어졌습니다. 삭제해주겠습니다.

```JAVASCRIPT
class Clock extends React.Component {
  // 새 constructor를 만들어 초기 state를 설정해 봅시다.
  constructor(props) { // 클래스 컴포넌트는 항상 props로 기본 constructor를 호출해야 합니다.
    super(props);
    this.state = {date: new Date()};
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2> {/*props를 state로 지정하여 콤포넌트내에서 제어할 수 있도록 합니다.*/}
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);

```

## 3 - 2) Lifecycle

### 마운트(mount)

Clock이 처음 DOM에 렌더링 될 때마다 타이머를 설정하려고 합니다. 이것을 React에서 “마운팅”이라고 합니다. 또한 Clock에 의해 생성된 DOM이 삭제될 때마다 타이머를 해제하려고 합니다.

>즉, Component가 새롭게 생성되는 시점이다. Component 함수가 실행되고 결과물로 나온 Element들이 가상 DOM에 삽입되고 실제 DOM을 업데이트하기까지의 과정이다.

컴포넌트 클래스에서 특별한 메서드를 선언하여 컴포넌트가 마운트되거나 언마운트 될 때 일부 코드를 작동할 수 있습니다.

_*많은 컴포넌트가 있는 애플리케이션에서 컴포넌트가 삭제될 때 해당 컴포넌트가 사용 중이던 리소스를 확보하는 것이 중요합니다._

#### 마운팅 메서드 추가
```JAVASCRIPT
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
  }

  componentWillUnmount() {
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}
```

### 생명주기(lifecycle)

마운트관련 메서드들은 “lifecycle 메서드”라고 불립니다.

|메서드종류|설명|
|:---:|:---:|
| componentDidMount() |  render 된 후에 실행됩니다. 외부의 데이터를 불러오거나 네트워크 요청을 보내야하는 경우에 사용됩니다. |
| componentDidUpdate() | update 가 이루어지고 render가 완료된 직후 실행되는 메서드입니다. 최초 마운트 될 때는 실행되지 않습니다. |
| componentWillUnmount() | 최종적으로 제거가 되기 전 실행이 된다. component 내에서 이루어지는 네트워크 요청, 타이머 이벤트 등 지속적으로 이루어지는 이벤트들을 해제하는데 유용하게 사용됩니다. |

componentDidMount() 메서드는 컴포넌트 출력물이 DOM에 렌더링 된 후에 실행됩니다. 이 장소가 타이머를 설정하기에 좋은 장소입니다.

#### componentDidMount()
```JAVASCRIPT
  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }
```

타이머가 끝난 dom을 unmount시키도록 하겠습니다.

#### componentWillUnmount()
```JAVASCRIPT
  componentWillUnmount() {
    clearInterval(this.timerID);
  }
```

마지막으로 Clock 컴포넌트가 매초 작동하도록 하는 tick()이라는 메서드를 구현해 보겠습니다.

이것은 컴포넌트 로컬 state를 업데이트하기 위해 this.setState()를 사용합니다.

```JAVASCRIPT
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

ReactDOM.render(
  <Clock />,
  document.getElementById('root')
);

```

> 다시 한번 복습해 보겠습니다.
> 1. Clock 콤포넌트가 ReactDOM.render()로 전달되었을 때 React는 Clock 컴포넌트의 constructor를 호출합니다. Clock이 현재 시각을 표시해야 하기 때문에 현재 시각이 포함된 객체로 this.state를 초기화합니다. 나중에 이 state를 업데이트할 것입니다.
> 2. React는 Clock 컴포넌트의 render() 메서드를 호출합니다. 이를 통해 React는 화면에 표시되어야 할 내용을 알게 됩니다. 그 다음 React는 Clock의 렌더링 출력값을 일치시키기 위해 DOM을 업데이트합니다.
> 3. Clock 출력값이 DOM에 삽입되면, React는 componentDidMount() 생명주기 메서드를 호출합니다. 그 안에서 Clock 컴포넌트는 매초 컴포넌트의 tick() 메서드를 호출하기 위한 타이머를 설정하도록 브라우저에 요청합니다.
> 4. 매초 브라우저가 tick() 메서드를 호출합니다. 그 안에서 Clock 컴포넌트는 setState()에 현재 시각을 포함하는 객체를 호출하면서 UI 업데이트를 진행합니다. 
> 5. setState() 호출 덕분에 React는 state가 변경된 것을 인지하고 화면에 표시될 내용을 알아내기 위해 render() 메서드를 다시 호출합니다. 이 때 render() 메서드 안의 this.state.date가 달라지고 렌더링 출력값은 업데이트된 시각을 포함합니다. React는 이에 따라 DOM을 업데이트합니다.
> 6. Clock 컴포넌트가 DOM으로부터 한 번이라도 삭제된 적이 있다면 React는 타이머를 멈추기 위해 componentWillUnmount() 생명주기 메서드를 호출합니다.

### 주의할 점

1. 직접 State를 수정하지 마세요. 대신 setState를 수정하여야 합니다.
2. State 업데이트는 비동기적일 수도 있습니다.
3. State 업데이트는 병합됩니다.
4. 컴포넌트는 자신의 state를 자식 컴포넌트에 props로 전달할 수 있습니다.

## 3 - 3) 하향식 데이터 흐름

하향식 데이터 흐름은 “단방향식” 데이터 흐름이라고 합니다. 모든 state는 항상 특정한 컴포넌트가 소유하고 있으며 그 state로부터 파생된 UI 또는 데이터는 오직 트리구조에서 자신의 “아래”에 있는 컴포넌트에만 영향을 미칩니다.

트리구조가 props들의 폭포라고 상상하면 각 컴포넌트의 state는 임의의 점에서 만나지만 동시에 아래로 흐르는 부가적인 수원(water source)이라고 할 수 있습니다.

모든 컴포넌트가 완전히 독립적이라는 것을 보여주기 위해 App 렌더링하는 세 개의 <Clock>을 만들었습니다.

```JAVASCRIPT
class Clock extends React.Component {
  constructor(props) {
    super(props);
    this.state = {date: new Date()};
  }

  componentDidMount() {
    this.timerID = setInterval(
      () => this.tick(),
      1000
    );
  }

  componentWillUnmount() {
    clearInterval(this.timerID);
  }

  tick() {
    this.setState({
      date: new Date()
    });
  }

  render() {
    return (
      <div>
        <h1>Hello, world!</h1>
        <h2>It is {this.state.date.toLocaleTimeString()}.</h2>
      </div>
    );
  }
}

function App() {
  return (
    <div>
      <Clock />
      <Clock />
      <Clock />
    </div>
  );
}

ReactDOM.render(
  <App />,
  document.getElementById('root')
);
```

## 3 - 4) 제어 컴포넌트

HTML에서 input, textarea, select와 같은 폼 엘리먼트는 일반적으로 사용자의 입력을 기반으로 자신의 state를 관리하고 업데이트합니다. React에서는 변경할 수 있는 state가 일반적으로 컴포넌트의 state 속성에 유지되며 setState()에 의해 업데이트됩니다.

그리고 폼을 렌더링하는 React 컴포넌트는 폼에 발생하는 사용자 입력값을 제어합니다. 이러한 방식으로 React에 의해 값이 제어되는 입력 폼 엘리먼트를 “제어 컴포넌트 (controlled component)“라고 합니다.

#### 예시 제어 콤포넌트
```JAVASCRIPT
class NameForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: ''};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('A name was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Name:
          <input type="text" value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

React state를 업데이트하기 위해 모든 키 입력에서 handleChange가 동작하기 때문에 사용자가 입력할 때 보여지는 값이 업데이트됩니다.

제어 컴포넌트로 사용하면, input의 값은 항상 React state에 의해 결정됩니다. 코드를 조금 더 작성해야 한다는 의미이지만, 다른 UI 엘리먼트에 input의 값을 전달하거나 다른 이벤트 핸들러에서 값을 재설정할 수 있습니다.

### textarea

React에서 textarea는 value 어트리뷰트를 대신 사용합니다. 이렇게하면 textarea를 사용하는 폼은 한 줄 입력을 사용하는 폼과 비슷하게 작성할 수 있습니다.

```JAVASCRIPT
class EssayForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      value: 'Please write an essay about your favorite DOM element.'
    };

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('An essay was submitted: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Essay:
          <textarea value={this.state.value} onChange={this.handleChange} />
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

### select

HTML에서 select는 드롭 다운 목록을 만듭니다. 예를 들어, 이 HTML은 과일 드롭 다운 목록을 만듭니다.

selected 옵션이 있으므로 Coconut 옵션이 초기값이 되는 점을 주의해주세요. React에서는 selected 어트리뷰트를 사용하는 대신 최상단 select태그에 value 어트리뷰트를 사용합니다. 한 곳에서 업데이트만 하면되기 때문에 제어 컴포넌트에서 사용하기 더 편합니다. 

#### 예시
```JAVASCRIPT
class FlavorForm extends React.Component {
  constructor(props) {
    super(props);
    this.state = {value: 'coconut'};

    this.handleChange = this.handleChange.bind(this);
    this.handleSubmit = this.handleSubmit.bind(this);
  }

  handleChange(event) {
    this.setState({value: event.target.value});
  }

  handleSubmit(event) {
    alert('Your favorite flavor is: ' + this.state.value);
    event.preventDefault();
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Pick your favorite flavor:
          <select value={this.state.value} onChange={this.handleChange}>
            <option value="grapefruit">Grapefruit</option>
            <option value="lime">Lime</option>
            <option value="coconut">Coconut</option>
            <option value="mango">Mango</option>
          </select>
        </label>
        <input type="submit" value="Submit" />
      </form>
    );
  }
}
```

_*select 태그에 multiple 옵션을 허용한다면 value 어트리뷰트에 배열을 전달할 수 있습니다._



여러 input 엘리먼트를 제어해야할 때, 각 엘리먼트에 name 어트리뷰트를 추가하고 event.target.name 값을 통해 핸들러가 어떤 작업을 할 지 선택할 수 있게 해줍니다.

#### 다중입력 제어
```JAVASCRIPT
class Reservation extends React.Component {
  constructor(props) {
    super(props);
    this.state = {
      isGoing: true,
      numberOfGuests: 2
    };

    this.handleInputChange = this.handleInputChange.bind(this);
  }

  handleInputChange(event) {
    const target = event.target;
    const value = target.name === 'isGoing' ? target.checked : target.value;
    const name = target.name;

    this.setState({
      [name]: value
    });
  }

  render() {
    return (
      <form>
        <label>
          Is going:
          <input
            name="isGoing"
            type="checkbox"
            checked={this.state.isGoing}
            onChange={this.handleInputChange} />
        </label>
        <br />
        <label>
          Number of guests:
          <input
            name="numberOfGuests"
            type="number"
            value={this.state.numberOfGuests}
            onChange={this.handleInputChange} />
        </label>
      </form>
    );
  }
}
```

전반적으로 input:text, textarea, select 모두 매우 비슷하게 동작합니다. 모두 제어 컴포넌트를 구현하는데 value 어트리뷰트를 허용합니다.

_* input:file은 특수하게 비제어 콤포넌트입니다._

>제어 컴포넌트의 대안
데이터를 변경할 수 있는 모든 방법에 대해 이벤트 핸들러를 작성하고 React 컴포넌트를 통해 모든 입력 상태를 연결해야 하기 때문에 때로는 제어 컴포넌트를 사용하는 게 지루할 수 있습니다. 특히 기존의 코드베이스를 React로 변경하고자 할 때나 React가 아닌 라이브러리와 React 애플리케이션을 통합하고자 할 때 짜증날 수 있습니다. 이러한 경우에 입력 폼을 구현하기 위한 대체 기술인 비제어 컴포넌트를 확인할 수 있습니다.

### 비제어 콤포넌트

React에서 input:file은 프로그래밍적으로 값을 설정 할 수 없고 사용자만이 값을 설정할 수 있기때문에 항상 비제어 컴포넌트입니다.

파일 API를 사용하여 파일과 상호작용해야 합니다.

#### 파일에 접근하기 위한 ref
```JAVASCRIPT
class FileInput extends React.Component {
  constructor(props) {
    super(props);
    this.handleSubmit = this.handleSubmit.bind(this);
    this.fileInput = React.createRef();
  }
  handleSubmit(event) {
    event.preventDefault();
    alert(
      `Selected file - ${this.fileInput.current.files[0].name}`
    );
  }

  render() {
    return (
      <form onSubmit={this.handleSubmit}>
        <label>
          Upload file:
          <input type="file" ref={this.fileInput} />
        </label>
        <br />
        <button type="submit">Submit</button>
      </form>
    );
  }
}

ReactDOM.render(
  <FileInput />,
  document.getElementById('root')
);
```

*** 
