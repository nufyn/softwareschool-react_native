# 2장. 데이터(Data)와 변수(Variable)

## 2 - 1) javascripts 데이터 타입

타입(data type)이란 프로그램에서 다룰 수 있는 값의 종류를 의미합니다.
자바스크립트에서는 여러 가지 형태의 타입을 미리 정의하여 제공하고 있으며, 이것을 기본 타입이라고 합니다.
자바스크립트의 기본 타입은 크게 __value(일반형)__ 와 __reference(참조형)__ 으로 구분할 수 있습니다.

_*C언어와 java는 데이터타입에 엄격하지만, 자바스크립트는 관대한 편임._

<br>

#### 데이터타입의 종류
| 분류 | 데이터형 | 의미 |
|---|:---:|:---:|
| value | number | 수 |
| value | string | "", ''로 감싸진 0개 이상의 문자열|
| value | boolean | true / false|
| value | null/undefined | 값이 없음 |
| value | 심볼(symbol) | ECMAScript 6부터 제공됨. 객체의 프로퍼티를 위한 식별자로 사용할 수 있습니다. |
| reference | array | 배열, 데이터들의 집합. |
| reference | function | 함수, 정해진 연산의 처리 |
| reference | object | 객체 |

>심볼 타입은 익스플로러에서 지원하지 않습니다.

<br/>

## 2 - 2) 숫자 데이터 타입

#### number
```JAVASCRIPT
var firstNum = 10;     // 소수점을 사용하지 않은 표현

var secondNum = 10.00; // 소수점을 사용한 표현

var thirdNum = 10e6;   // 10000000

var fourthNum = 10e-6; // 0.00001
```

<br/>

## 2 - 3) 문자열 데이터 타입

#### string
```JAVASCRIPT
var firstStr = "이것도 문자열입니다.";      // 큰따옴표를 사용한 문자열

var secondStr = '이것도 문자열입니다.';     // 작은따옴표를 사용한 문자열

var thirdStr = "나의 이름은 '홍길동'이야."  // 작은따옴표는 큰따옴표로 둘러싸인 문자열에만 포함될 수 있음.

var fourthStr = '나의 이름은 "홍길동"이야.' // 큰따옴표는 작은따옴표로 둘러싸인 문자열에만 포함될 수 있음.
```

<br/>

### 문자열 데이터 연산

#### string
```JAVASCRIPT
var str1 = "Hello";
var str2 = "World!";

document.getElementById("result").innerHTML = (str1 + str2);
```

### 문자열과 숫자 데이터의 연산

#### 문자열과 숫자
```JAVASCRIPT
var str = "lee jung";

var num = 1;

document.getElementById("result").innerHTML = (str + num); // 이정원

var res = "3" * "5";     // 곱셈 연산을 위해 두 문자열이 모두 숫자로 변환됨.

var not_a_number = 1 - "string";  // NaN
```

>NaN은 Not a Number의 축약형으로, 정의되지 않은 값이나 표현할 수 없는 값이라는 의미를 가집니다.
이러한 NaN은 Number 타입의 값으로 0을 0으로 나누거나, 숫자로 변환할 수 없는 피연산자로 산술 연산을 시도하는 경우에 반환되는 읽기 전용 값입니다.

<br/>

### 숫자를 문자열로 반환

- toExponential()
- toFixed()
- toPrecision()

| 메서드 | 설명 |
|---|:---:|
|toExponential()|정수 부분은 1자리, 소수 부분은 입력받은 수만큼 e 표기법을 사용하여 숫자를 문자열로 변환함.|
|toFixed()|소수 부분을 입력받은 수만큼 사용하여 숫자를 문자열로 변환함.|
|toPrecision()|입력받은 수만큼 유효 자릿수를 사용하여 숫자를 문자열로 변환함.|

<br/>

### 날짜를 숫자 데이터로 반환

| 메서드 | 설명 |
|---|:---:|
|getDate()|날짜 중 일자를 숫자로 반환함. (1 ~ 31)|
|getDay()|날짜 중 요일을 숫자로 반환함. (일요일 : 0 ~ 토요일 : 6)|
|getFullYear()|날짜 중 연도를 4자리 숫자로 반환함. (yyyy년)|
|getMonth()|날짜 중 월을 숫자로 반환함. (1월 : 0 ~ 12월 : 11)|
|getTime()|1970년 1월 1일부터 현재까지의 시간을 밀리초(millisecond) 단위의 숫자로 반환함.|
|getHours()|시간 중 시를 숫자로 반환함. (0 ~ 23)|

>날짜데이터는 문자열과 숫자로 변환할 수 있는 유일한 데이터타입임

### + 다른 데이터를 문자열로 반환

- String()
- toString()

<br/>

## 2 - 4) 불리언 데이터 타입

#### boolean
```JAVASCRIPT
var firstNum = 10;
var secondNum = 11;

document.getElementById("result").innerHTML = (firstNum == secondNum); // false
```

_*boolean 데이터 타입은 주로 비교연산자, 제어문과 함께 사용됩니다._

<br/>

## 2 - 5) 널 데이터 타입

#### null
```JAVASCRIPT
var num;          // 초기화하지 않았으므로 undefined 값을 반환함.

var str = null;   // object 타입의 null 값

typeof secondNum; // 정의되지 않은 변수에 접근하면 undefined 값을 반환함.
```

<br/>

## 2 - 6) 데이터 알아내기

#### typeof 연산자

```JAVASCRIPT
typeof 10;        // number 타입

typeof "문자열";  // string 타입

typeof true;      // boolean 타입

typeof undefined; // undefined 타입

typeof null;      // object 타입
```

<br/>

## 2 - 6) 변수의 유효범위

- 지역변수(local variable)
- 전역변수(global variable)

### 지역변수(local variable)

지역변수는 함수내에서만 사용가능한 변수를 뜻합니다.

이러한 지역 변수는 변수가 선언된 함수 내에서만 유효하며, 함수가 종료되면 메모리에서 사라집니다.
함수의 매개변수 또한 함수 내에서 정의되는 지역 변수처럼 동작합니다.

자바스크립트에서는 선언되지 않은 변수를 사용하려고 하거나 접근하려고 하면 오류를 발생시킵니다.
하지만 선언되지 않은 변수에 대한 typeof 연산자의 결괏값은 undefined 값을 반환합니다.

### 전역변수(global variable)

전역변수는 함수 외부에서 선언된 변수입니다.
프로그램중의 어느 곳에나 전역적으로 사용할 수 있으며 할당된 메모리는 프로그램(js에선 웹앱)이 종료되면 지워집니다. 

#### 퀴즈) 값이 20인 num을 찾으시오

```JAVASCRIPT
var num = 10; // 전역 변수 num을 선언함.

function globalNum() {

    document.write("함수 내부에서 변수 num의 값은 " + num + "입니다.<br>");

    num = 20; // 전역 변수 num의 값을 함수 내부에서 변경함.

}

globalNum();  // 함수 globalNum()을 호출함.

document.write("함수의 호출이 끝난 뒤 변수 num의 값은 " + num + "입니다.");
```

```JAVASCRIPT
var num = 10; // 전역 변수 num을 선언함.

function globalNum() {
    var num = 20; // 전역 변수 num의 값을 함수 내부에서 변경함.
    document.write("함수 내부에서 변수 num의 값은 " + num + "입니다.<br>");
}

globalNum();  // 함수 globalNum()을 호출함.

document.write("함수의 호출이 끝난 뒤 변수 num의 값은 " + num + "입니다.");
```

***
