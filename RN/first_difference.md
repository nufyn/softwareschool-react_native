# react와 react-native의 차이점

## 1 - 1) 특징

### React

Reactjs는 사용자 인터페이스 및 웹앱 구축을 위해 프론트엔드 딴과 서버에서 실행되는 백엔드딴을 지원하는 js의 라이브러리입니다. 주로 하는 역할은 SPA(single page app)의 구현을 쉽게 할 수 있게 하는 것 입니다.

### ReactNative

기본 앱 구성 요소로 컴파일되는 모바일 프레임워크로 Reactjs를 사용하여 구성요소를 빌드합니다.

_*라이브러리와 프레임워크의 차이는 자유도의 차이가 제일 크게 실감됩니다. 사실 그 차이는 프레임워크가 뜻하는 것이 강한 틀이라는 것과 라이브러리가 뜻하는 여러 도구들의 모음집이라는 말의 뜻의 차이정도 입니다._

## 1 - 2) 쓰임 

### React 

React는 javascript와 jsx를 사용하여 웹앱에 뷰를 렌더링하는 UI 라이브러리입니다.

### ReactNative

ReactNative는 React의 추가 라이브러리중 하나이며, 모바일 앱(ios, android)을 만듭니다.

## 1 - 3) design

둘은 닮은 듯 안 닮은 듯한 코드 디자인을 가지고 있습니다. 

#### React
```JAVASCRIPT
import React from 'react';
import ReactDOM from 'react-dom';

class HelloMessage extends React.Component {
  render() {
    return (
      <div>
        Hello {this.props.name}
      </div>
    );
  }
}

ReactDOM.render(
  <HelloMessage name="Taylor" />,
  document.getElementById('hello-example')
);
```

#### ReactNative
```JAVASCRIPT
import React from 'react';
import {Text, View} from 'react-native';

const WelcomeScreen = () =>
  <View>
    <Text>
      Edit App.js to change this screen and turn it
      into your app.
    </Text>
   </View>
```

여기서 또 다른 점은 React의 코드에서는 익숙한 html코드같아 보이는 구문이 보이는 반면, ReactNative는 View와 Text라고 새로운 태그를 보여주고 있습니다. 이렇게 놓고 보면 둘은 서로 다른것 같아 보이지만, React를 학습한 후에 보시면 '똑같구나'라고 생각하시게 될겁니다.

_*이 외에도 styling과 사용가능한 ribrary의 종류등이 다릅니다._

***
