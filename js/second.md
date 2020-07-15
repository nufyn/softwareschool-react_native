# 2 - 1장. javascripts 데이터 타입

타입(data type)이란 프로그램에서 다룰 수 있는 값의 종류를 의미합니다.
<br/>
자바스크립트에서는 여러 가지 형태의 타입을 미리 정의하여 제공하고 있으며, 이것을 기본 타입이라고 합니다.
<br/>
자바스크립트의 기본 타입은 크게 __value__와 __reference__으로 구분할 수 있습니다.
<br/>

*C언어와 java는 데이터타입에 엄격하지만, 자바스크립트는 관대한 편임.

### 데이터타입의 종류

| 분류 | 데이터형 | 의미 |
|---|:---:|:---:|
| value | number | 수 |
|  | string | "", ''로 감싸진 0개 이상의 문자열|
|  | boolean | true / false|
|  | null/undefined | 값이 없음 |
|  | 심볼(symbol) | ECMAScript 6부터 제공됨. 객체의 프로퍼티를 위한 식별자로 사용할 수 있습니다. |
| reference | array | 배열 |
|  | function | 함수 |
|  | object | 객체 |

<blockquote>심볼 타입은 익스플로러에서 지원하지 않습니다.</blockquote>

<br/>

# 2 - 2장. 숫자 데이터 타입 

```javascript
var firstNum = 10;     // 소수점을 사용하지 않은 표현

var secondNum = 10.00; // 소수점을 사용한 표현

var thirdNum = 10e6;   // 10000000

var fourthNum = 10e-6; // 0.00001
```

<br/>

# 2 - 3장. 문자열 데이터 타입

```javascript
var firstStr = "이것도 문자열입니다.";      // 큰따옴표를 사용한 문자열

var secondStr = '이것도 문자열입니다.';     // 작은따옴표를 사용한 문자열

var thirdStr = "나의 이름은 '홍길동'이야."  // 작은따옴표는 큰따옴표로 둘러싸인 문자열에만 포함될 수 있음.

var fourthStr = '나의 이름은 "홍길동"이야.' // 큰따옴표는 작은따옴표로 둘러싸인 문자열에만 포함될 수 있음.
```

### 문자열 데이터 연산

```javascript
var str1 = "Hello";
var str2 = "World!";

document.getElementById("result").innerHTML = (str1 + str2);

```

### 문자열과 숫자 데이터의 연산

```javascript
var str = "lee jung";

var num = 1;

document.getElementById("result").innerHTML = (str + num); // 이정원

var res = "3" * "5";     // 곱셈 연산을 위해 두 문자열이 모두 숫자로 변환됨.

var not_a_number = 1 - "string";  // NaN
```

<blockquote>NaN은 Not a Number의 축약형으로, 정의되지 않은 값이나 표현할 수 없는 값이라는 의미를 가집니다.<br/>
이러한 NaN은 Number 타입의 값으로 0을 0으로 나누거나, 숫자로 변환할 수 없는 피연산자로 산술 연산을 시도하는 경우에 반환되는 읽기 전용 값입니다.</blockqupte>

<br/>

### 숫자를 문자열로 반환

<ol>
    <li>toExponential()</li>
    <li>toFixed()</li>
    <li>toPrecision()</li>
</ol>

| 메소드 | 설명 |
|---|:---:|
|toExponential()|정수 부분은 1자리, 소수 부분은 입력받은 수만큼 e 표기법을 사용하여 숫자를 문자열로 변환함.|
|toFixed()|소수 부분을 입력받은 수만큼 사용하여 숫자를 문자열로 변환함.|
|toPrecision()|입력받은 수만큼 유효 자릿수를 사용하여 숫자를 문자열로 변환함.|

### 다른 데이터를 문자열로 반환

<ol>
    <li>String()</li>
    <li>toString()</li>
</ol>

### 날짜를 문자열로 반환

| 메소드 | 설명 |
|---|:---:|
|getDate()|날짜 중 일자를 숫자로 반환함. (1 ~ 31)|
|getDay()|날짜 중 요일을 숫자로 반환함. (일요일 : 0 ~ 토요일 : 6)|
|getFullYear()|날짜 중 연도를 4자리 숫자로 반환함. (yyyy년)|
|getMonth()|날짜 중 월을 숫자로 반환함. (1월 : 0 ~ 12월 : 11)|
|getTime()|1970년 1월 1일부터 현재까지의 시간을 밀리초(millisecond) 단위의 숫자로 반환함.|
|getHours()|시간 중 시를 숫자로 반환함. (0 ~ 23)|


getDate()	
getDay()	
getFullYear()	
getMonth()	
getTime()	
getHours()	
getMinutes()	시간 중 분을 숫자로 반환함. (0 ~ 59)
getSeconds()	시간 중 초를 숫자로 반환함. (0 ~ 59)
getMilliseconds()	시간 중 초를 밀리초(millisecond) 단위의 숫자로 반환함. (0 ~ 999)

# 2 - 4장. 불리언 데이터 타입

```javascript
var firstNum = 10;
var secondNum = 11;

document.getElementById("result").innerHTML = (firstNum == secondNum); // false
```

<blockquote>boolean 데이터 타입은 주로 비교연산자, 제어문과 함께 사용됩니다.</blockquote>

<br/>

# 2 - 5장. 널 데이터 타입

```javascript
var num;          // 초기화하지 않았으므로 undefined 값을 반환함.

var str = null;   // object 타입의 null 값

typeof secondNum; // 정의되지 않은 변수에 접근하면 undefined 값을 반환함.
```

<br/>

# 2 - 5장. 데이터 알아내기

### typeof 연산자

```javascript
typeof 10;        // number 타입

typeof "문자열";  // string 타입

typeof true;      // boolean 타입

typeof undefined; // undefined 타입

typeof null;      // object 타입
```

<br/>

***