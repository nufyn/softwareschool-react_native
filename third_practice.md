# 3장. 테스트

코드의 의미는 몰라도 됩니다. 적어도 지금은요. 실습환경이 제대로 잘 설정되었는지, 그리고 앞으로 죽 봐야할 코드에 대해 친숙해지는 시간입니다.

## 3 - 1) react

#### 초기화면

![1](./2.jpg)

처음에 npm start해서 보았던 화면을 기억하시죠?

my-app/ 디렉토리안에 src/App.js를 보시면 header 태그가 있습니다. header태그 내부를 다 지워주시면 아무것도 없는 흰 바탕이 나옵니다.

```JAVASCRIPT
import React from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header"> 
        <img src={logo} className="App-logo" alt="logo" /> {/** 여기 header태그 안을 다 지워주세요 */}
        <p>
          Edit <code>src/App.js</code> and save to reload.
        </p>
        <a
          className="App-link"
          href="https://reactjs.org"
          target="_blank"
          rel="noopener noreferrer"
        >
          Learn React
        </a>
      </header>
    </div>
  );
}

export default App;
```

그리고 나서 가장 기본적인 Hello world!!! 출력을 해봅시다.

```JAVASCRIPT
import React from 'react';
import logo from './logo.svg';
import './App.css';

function App() {
  return (
    <div className="App">
      <header className="App-header"> 
        Hello world!!!
      </header>
    </div>
  );
}

export default App;
```

![5](./5.jpg)

이쁘네요!

<br/>

## 3 - 2) React-Native

리액트 네이티브 테스트를 위해 방금전 설치한 expo-cli app을 각자의 로컬 디바이스에서 구동시켜 보겠습니다. android-studio emulator 를 사용하실 분들은 emulator를 따로 구동해 주세요.

![2](./2.png)

저기보이는 qr코드를 모바일에 설치된 expo앱에 인식시킵니다. 각자 앱스토어에서 expo를 다운받아 사용해보세요.

![21](./11.jpg)

혹은 팝업된 웹에 qr코드를 인식하여도 됩니다.

![3](./3.jpg)

성공 하셨나요?

![4](./8.jpg)

이제 가장 기초적인 테스트이자 가장 유명한 구문 hello world!를 렌더 시켜보겠습니다.

![5](./3.png)

***
