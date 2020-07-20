# ReactNative 

## 1 - 1) 리액트 네이티브는 Reactjs와 달리 css가 없습니다.

ReactNative는 프레임워크라는 특성때문에 자유도가 높지 못합니다. 바로 규격이 있다는 것입니다. React에서는 html의 모든 태그를 다 사용하고, css는 물론, scss까지 사용이 가능했었는데, ReactNative는 전혀 그렇지 못합니다. 사용할 수 있는 건 View와 Text, 그리고 inline styling뿐이죠. 대신 ReactNative에는 엄청나게 많고 훌륭한 Component들과 API들이 있습니다. 그들 덕분에 쉽고 예쁘게 뷰를 렌더링할 수 있습니다.

#### inline style
```JAVASCRIPT
import { StyleSheet } from 'react-native'; 

const styles = StyleSheet.create({
  textStyle: {
    fontSize: 20,
  },
  otherStyle: {
    position: 'absolute',
    justifyContent: 'center',
  }
});
```

css가 없어짐과 동시에 html에 클래스속성이 사라집니다. 그리하여 사람들은 동적으로 요소들을 컨트롤할 수 있는 다른 속성이 필요했고, 그로인해 구조가 조금씩 React와 달라지기 시작합니다. 그로인해 앱의 구상/설계 단계에서 부터 React와 다른 길을 걷게 됩니다.

## 1 - 2) CoreComponents

### View

View는 ReactNative의 코어컴포넌트중 하나로, html에서 div만큼이나 자주 쓰이는 녀석입니다. 형제로는 ScrollView가 있으며, 둘의 쓰임은 둘 다 div같은 요소를 감싸는 존재지만, ScrollView의 경우 이름에서도 알 수 있듯이 스크롤이 가능한 View입니다. 

### Text

Text 컴포넌트는 html의 p를 대신하는 컴포넌트입니다. 주로 하는 역할은 텍스트의 표시, 스타일 및 중첩 문자열과 터치 이벤트 처리등 입니다.

#### 표

|default| android|ios|web|설명|
|:---:|:---:|:---:|:---:|:---:|
|`<View>`|`<ViewGroup>`|`<UIView>`|`<div>`|flexbox, 스타일, 터치 처리 및 접근성 제어 기능이 있는 레이아웃을 지원하는 컨테이너|
|`<ScrollView>`|`<ViewGroup>`|`<UIView>`|`<div>`|여러 구성 요소 및 보기를 포함할 수 있는 일반 스크롤 컨테이너|
|`<Text>`|`<ViewGroup>`|`<UIView>`|`<div>`|텍스트의 표시, 스타일 및 중첩 문자열과 터치 이벤트 처리|
|`<TextInput>`|`<ViewGroup>`|`<UIView>`|`<div>`|사용자가 텍스트를 입력할 수 있습니다.|
|`<Image>`|`<ViewGroup>`|`<UIView>`|`<div>`|다양한 유형의 이미지를 표시합니다.|

***