# 수업 소개

## 1 - 1) Android 소개

### 안드로이드의 역사

2003년 10월에 Palo Alto, California에서 Android사가 설립되었습니다.
초기에는 디지털 카메라용 OS를 개발하는 회사였는데, MS의 윈도우즈 모바일과 심비안에 대항하는 휴대전화용 OS를 개발하였습니다.
그리고 2005년 7월, Google이 Android사를 5,000만 달러에 인수합니다.
2007년 11월 5일 안드로이드 플랫폼을 휴대폰 운영 체제로서 무료로 공개한다고 발표한 후, 구글, 디바이스 제작사, 통신사, 칩셋 제작사들이 모인 Open Handset Alliance에서 공개 표준을 위해 개발하고 있습니다.


### 안드로이드의 구성

### Linux Kernel

안드로이드의 커널은 리눅스 커널의 장기 지원(LTS) 버전을 기반으로 개발되었습니다. 2017년 기준, 안드로이드 기기들은 주로 Linux 커널의 3.18 또는 4.4 버전을 사용중이라고 합니다. 실제 커널은 개별 디바이스별로 상이하고, Google에 의해 추가적인 아키텍쳐 변경이 이루어진다고 합니다.

<br/>

### Hardware Abstraction Layer(HAL)

상위 레벨 Java API 프레임워크에 하드웨어 기능을 제공하는 표준 인터페이스를 제공합니다.
카메라, 블루투스, 오디오 등과 같은 여러가지 라이브러리들로 구성되어 있습니다.

<br/>

### Native C/C++ Libraries

Webkit, OpenGL ES 등의 고유 라이브러리를 제공하기 위한 Java 프레임워크 API를 제공합니다.
예를 들어, Android 프레임워크의 Java OpenGL API를 통해 2D/3D 그래픽을 다루는 OpenGL ES를 사용할 수 있습니다.
C/C++을 사용하여 개발할 경우, Android NDk를 이용해서 native 라이브러리를 직접 사용할 수 있습니다.

<br/>

### Android Runtime (ART)

안드로이드 5.0 이상부터 각각의 앱들은 Android Runtime(ART)으로 개별 프로세스 형태로 동작합니다.
안드로이드 5.0 이하에서는 Dalvik runtime을 사용합니다.

>### Android Runtime(ART)
>- Ahead-of-time(AOT) + just-in-time(JIT) compilation
>- Optimized garbage collection (GC)
>### Dalvik
>- Trace-based just-in-time (JIT) compilation
>- 지속적으로 어플리케이션을 프로파일링해서, 자주 사용되는 segment를 native 기계어로 미리 컴파일함.


개발한 어플리케이션이 ART에서 정상적으로 동작한다면, Dalvik에서도 정상적으로 동작한다.

하지만 그 반대는 항상 정상적으로 동작하지 않을 수도 있다.

<br/>

### Java API Framework

안드로이드 OS의 모든 기능들은 Java언어로 쓰여진 API들을 통해서 접근 가능합니다.

#### API
| API | 설명|
|:--:|:--:|
|View System|리스트, 그리드, 텍스트박스, 버튼 및 웹브라우저 등의 어플리케이션의 UI를 구성합니다.|
|Resource Manager|Localized 문자열, 그래픽 및 레이아웃 파일등과 같은 코드 이외의 자원들에 접근하는 기능을 제공합니다.|
|Notification Manager|상태바에 커스텀 열람 기능을 제공합니다.|
|Activity Manager|어플리케이션의 lifecycle을 관리하고 일반적인 navigation back 스택을 관리합니다.|
|Content Provider|다른 어플리케이션의 데이터에 접근하고 데이터를 공유하는 기능을 제공합니다.|
|Package Manager|현재 디바이스에 설치된 어플리케이션 패키지와 관련된 다양한 정보들을 관리합니다.|

<br/>

### System Apps

E-mail, SMS, Calendar, 인터넷 브라우저 및 연락처 등의 어플리케이션

## 1 - 2) Reactjs + ReactNative

### Reactjs

Facebook에서 마음먹고 개발한 React.js는 요새 웹사이트 개발을 할 때 가장 많이 쓰이는 라이브러리 중 하나입니다. 
Facebook, Instagram, Uber, Evernote 등 짱짱한 기업들이 React를 도입했다고 하니 충분히 검증됐다고 봐도 되겠습니다. 

React.js가 현재 프론트엔드 개발자들의 사랑을 받게된 이유는 유연하다는 점입니다. Angular.js 같은 프레임워크가 아닌 라이브러리이기 때문에 필요에 따라 붙이고 뗄 수 있습니다. 하지만 반대로 이 말은 웹을 만드는데 꼭 필요한 도구를 제공해주지 않는다는 것입니다. 그 대신 React는 규칙(컴퍼넌트, JSX)을 제공해 줍니다. 이 규칙들을 통해 개발자는 React 이전의 대세인 Jquery보다 더 효율적이고 가볍게 웹을 제작할 수 있게 되었습니다.

즉, React는 언어라기 보단 일종의 javascript를 쓰는 __개념__ 입니다.

### React-native

위에서 언급했던 React와 형제격의 프로젝트로 역시나 부모는 facebook입니다. 이름에서 예상했듯이 React Native는 리액트의 접근방법을 모바일로 확장한 Facebook의 오픈소스 프로젝트입니다. 쉽게 이야기하면 React의 규칙을 이용하여 모바일 어플리케이션 개발을 할 수 있다는 말입니다. 

일반적으로 '앱'을 개발하기 위해서는 안드로이드의 경우 Android(Java), 아이폰의 경우 IOS(Swift || Objective C) 를 사용해야 합니다. 이 때 안드로이드, IOS 개발을 따로 하는 경우 Native 개발을 한다고 이야기합니다. 그러나 빠르게 앱을 만들어 시장 반응을 보려 하는 스타트업과 같은 곳에서는 두가지를 동시에 개발하기에는 인력과 시간 소모가 크겠죠. 이에 Android , IOS 어플리케이션을 동시에 개발할 수 있는 하이브리드 앱이 나오게 되었습니다(대표적인 예로 Ionic). 그러나 하이브리드 앱의 경우 웹뷰를 네이티브에 씌우는 형태이기 때문에 속도가 느리고 큰 규모의 프로젝트에는 적합하지 않습니다.

### 우리가 해야할 프로젝트는?

저희는 지금부터 js를 알아보고, 실습해보며 react로 나아가기 위한 발판을 튼튼하게 할 것입니다. React는 javascript의 라이브러리이기 때문입니다. React를 모두 학습하고, React의 개념이 완벽히 정립되었을때, 우리는 React를 발판삼아 또 한 번의 도약을 해야합니다. 그것이 저희 최종목표, ReactNative입니다.

***
