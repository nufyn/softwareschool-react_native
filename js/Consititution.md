# 개요

<b>
소프트웨어학교 강의 자료
소프트웨어 고등학교 학생들을 위한 javascripts 기초 강의 자료<br/>
</b>

# 목차

<ol>
  <li>1장
    <ul>
      <li>자바스크립트 소개</li>
      <li>자바스크립트 개요</li>
      <li>자바스크립트 기초</li>
      <li>자바스크립트 문법</li>
      <li>자바스크립트 적용</li>
    </ul>
  </li>
</ol>

<br/>

***

<br/>

# 1 - 1장. javascripts 소개

<ul>
    <li>자바스크립트(JavaScript)는 객체(object) 기반의 스크립트 언어입니다.</li>
    <li>자바스크립트는 동적으로 웹의 동작을 구현할 수 있습니다. 이로인해 웹의 사용범위가 크게 늘어났습니다.</li>
    <li>자바스크립트로 할 수 있는 기능으로는 html의 속성과 태그를 수정하고, 내용을 변경하고, 스타일을 입힐 수 있습니다.<br/> 물론 사용자들의 동작을 바탕으로 모든 요소들을 바꿀 수 있습니다. </li>
    <li>자바스크립트는 주로 웹 브라우저에서 사용되나, Node.js와 같은 프레임워크를 사용하면 서버 측 프로그래밍에서도 사용할 수 있습니다.</li>
    <li>*언어 규격은 자바의 부분 집합(subset)으로 되어 있습니다만은 자바와는 다른 언어입니다.</li>
</ul>

<br/>

### 자바스크립트와 자바의 비교
| javascripts | java |
|:---:|:---:|
| 객체지향, 객체의 형 간에 차이 없음. 프로토타입 매커니즘을 통한 상속, 그리고 속성과 메소드는 어떤 객체든 동적으로 추가될 수 있음 | 클래스기반, 객체는 크래스 계층구조를 통한 모든 상속과 함께 클래스와 인스턴스로 나뉨.<br/> 클래스와 인스턴스는 동적으로 추가된 속성이나 메소드를 가질 수 없음 |
| 변수 자료형이 선언되지 않음. | 변수 자료형은 반드시 선언되어야 함. |
| 하드디스크에 자동으로 작성 불가. | 하드디스크에 자동으로 작성 가능. |

<br/>

# 1 - 2장. javascripts 개요

순수 자바스크립트의 함수 정의

```javascript
function nufynComeFunny() {
    document.getElementById("text").innerHTML = "Hello world!";
}

nufynComeFunny()
```

html내에서 자바스크립트의 모습

```html
<script>
    document.getElementById("text").innerHTML = "Hello world!";
</script>
```

<br/>

# 1 - 3장. javascripts 특징

자바스크립트는 다음과 같은 특징을 가집니다.

<ol>
    <li>자바스크립트는 객체 기반의 스크립트 언어입니다.</li>
    <li>자바스크립트는 동적이며, 타입을 명시할 필요가 없는 인터프리터 언어입니다.</li>
    <li>자바스크립트는 객체 지향형 프로그래밍과 함수형 프로그래밍을 모두 표현할 수 있습니다.</li>
</ol>

<blockquote>인터프리터 언어는 사용자가 실행할 수 있는 실행 파일(.exe)로 만드는 과정을 거치지 않고, 소스 코드를 바로 실행할 수 있는 언어를 의미합니다.</blockquote>

<br/>

# 1 - 4장. javascripts 문법

javascripts은 세미콜론으로 끝나는 것을 기본으로, 내장되어 있는 예약어(키워드)들과 식별자를 이용해서 프로그래밍하게 됩니다.

### 자주쓰는 기본 예약어
| 값 | 의미 | 기본값 |
|---|:---:|:---:|
| `var` | 변수 선언시, 재할당, 재선언 모두 가능 | 변수 정의 |
| `let` | es6에 추가된 변수 선언시, 변수 재선언은 불가능하지만, 재할당은 가능 | 변수 정의 |
| `const` | es6에 추가된 변수 선언시, 상수처럼 재선언, 재할당 모두 불가 | 변수 정의 |
| `class` | es2015에 추가된 클래스의 정의를 위해 예약된 키워드 | 클래스 정의 |
| `function` | 함수의 정의를 위해 예약된 키워드 | 함수 정의 |

그 밖에 string의 사용등에서 '' 보단 ""의 사용을 권장하며, 
<br/>
주석은 "//"와 "/** */"로 사용가능하지만, "/**/"를 권장합니다.
<br/>
식별자의 네이밍은 세가지 형태 __lowerCamelCase__, __UpperCamelCase(=PascalCase)__와 __snake_case(=underscore_case)__가 있습니다. 
<br/>
이는 자바스크립트의 아래의 규칙때문에 그렇습니다.

<blockquote>
자바스크립트에서 식별자는 숫자와 식별자의 구별을 빠르게 할 수 있도록 숫자로는 시작할 수 없습니다.
<br/>
자바스크립트에서 하이픈(-)은 뺄셈을 위해 예약된 키워드이므로, 식별자를 작성할 때는 사용할 수 없습니다.
</blockquote>

<br/>

# 1 - 5장. javascripts 적용

### html에 텍스트 출력하기

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <title>Nufyn</title>
        <script>
            document.write("<p>script는 html의 head태그안에 삽입할 수 있습니다.</p>")
        </script>
    </head>
    <body>
        <script>
            document.write("<h2>(권장!)혹은 body 닫는 태그의 바로 위에 삽입할 수도 있습니다.</h2>")
        </script>
    </body>
        <script>
            document.write("<h3>(권장하지 않음!)body태그 밖에 삽입해도 기능은 동작하지만, 권장하지 않습니다.</h3>")
        </script>
</html>
```

### 함수 정의 후, html에서 출력하기

```html
<!DOCTYPE html>
<html lang="ko">
    <head>
        <meta charset="UTF-8">
        <title>Nufyn</title>
        <script>
            function printDate() {
                document.getElementById("text").innerHTML = "지금은!";
                document.getElementById("date").innerHTML = Date();
            }
        </script>
    </head>
    <body>
        <button onclick="printDate()">시간알림 버튼</button>
        <h1 id="text">Hello world</h1>
        <p id="date"></p>
        <h2>입니다!</h2>
    </body>
</html>
```