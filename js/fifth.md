# 5장. 배열

***

## 5 - 1) 배열이란

자바스크립트에서 배열(array)은 이름과 인덱스로 참조되는 정렬된 값의 집합으로 정의됩니다.
배열을 구성하는 각각의 값을 배열 요소(element)라고 하며, 배열에서의 위치를 가리키는 숫자를 인덱스(index)라고 합니다.

자바스크립트에서 배열의 특징은 다음과 같습니다.

1. 배열 요소의 타입이 고정되어 있지 않으므로, 같은 배열에 있는 배열 요소끼리의 타입이 서로 다를 수도 있습니다.
2. 배열 요소의 인덱스가 연속적이지 않아도 되며, 따라서 특정 배열 요소가 비어 있을 수도 있습니다.
3. 자바스크립트에서 배열은 Array 객체로 다뤄집니다.

<br/>

## 5 - 2) 배열 생성

1. var arr = [배열요소1, 배열요소2,...];          // 배열 리터럴을 이용하는 방법
2. var arr = Array(배열요소1, 배열요소2,...);     // Array 객체의 생성자를 이용하는 방법
3. var arr = new Array(배열요소1, 배열요소2,...); // new 연산자를 이용한 Array 객체 생성 방법

```javascript
var arrLit = [1, true, "JavaScript"];             // 배열 리터럴을 이용하는 방법
var arrObj = Array(1, true, "JavaScript");        // Array 객체의 생성자를 이용하는 방법
var arrNewObj = new Array(1, true, "JavaScript"); // new 연산자를 이용한 Array 객체 생성 방법

document.write(arrLit + "<br>");                  // 1,true,JavaScript

document.write(arrObj + "<br>");                  // 1,true,JavaScript 

document.write(arrNewObj);                        // 1,true,JavaScript
```

<br/>

## 5 - 3) 배열의 참조

>배열이름[인덱스]

```javascript
var arr = ["JavaScript"]; // 요소가 하나뿐인 배열을 생성함.
var element = arr[0];     // 배열의 첫 번째 요소를 읽어서 대입함.

arr[1] = 10;      // 배열의 두 번째 요소에 숫자 10을 대입함. 배열의 길이는 1에서 2로 늘어남.
arr[2] = element; // 배열의 세 번째 요소에 변수 element의 값을 대입함. 배열의 길이는 2에서 3으로 늘어남.

document.write("배열 arr의 요소에는 [" + arr + "]가 있습니다.<br>"); // 배열의 요소를 모두 출력함.
document.write("배열 arr의 길이는 " + arr.length + "입니다.<br>");   // 배열의 길이를 출력함.

delete arr[2];    // 배열의 세 번째 요소를 삭제함. 하지만 배열의 길이는 변하지 않음.

document.write("배열 arr의 요소에는 [" + arr + "]가 있습니다.<br>"); // 배열의 요소를 모두 출력함.
document.write("배열 arr의 길이는 " + arr.length + "입니다.");       // 배열의 길이를 출력함.
```

<br/>

## 5 - 4) 배열 요소의 추가

1. arr.push(추가할 요소);         // push() 메소드를 이용하는 방법
2. arr[arr.length] = 추가할 요소; // length 프로퍼티를 이용하는 방법
3. arr[특정인덱스] = 추가할 요소; // 특정 인덱스를 지정하여 추가하는 방법

```javascript
var arr = [1, true, "Java"];

arr.push("Script");           // push() 메소드를 이용하는 방법

document.write(arr + "<br>"); // 1,true,Java,Script

arr[arr.length] = 100;        // length 프로퍼티를 이용하는 방법

document.write(arr + "<br>"); // 1,true,Java,Script,100

arr[10] = "자바스크립트";     // 특정 인덱스를 지정하여 추가하는 방법

document.write(arr + "<br>"); // 1,true,Java,Script,100,,,,,,자바스크립트

document.write(arr[7]);       // undefined
```

<br/>

## 5 - 5) 배열 탐색(요소 접근)

배열의 모든 요소에 차례대로 접근하고 싶을 때는 for문 혹은 for / in문 과 같은 반복문을 사용하여 접근할 수 있습니다.

```javascript
var arr = [1, true, "JavaScript"];

var result = "<ul>";

for (var idx in arr) {
    result += "<li>" + arr[idx] + "</li>";
}

result += "</ul>";

document.write(result);
```

<br/>

## 5 - 6) Array 객체

자바스크립트에서 배열(array)은 정렬된 값들의 집합으로 정의되며, Array 객체로 다뤄집니다.
또한, 자바스크립트는 사용자가 배열과 관련된 작업을 손쉽게 할 수 있도록 다양한 메소드도 제공하고 있습니다.

#### 배열과 배열요소의 타입
```javascript
var arr = new Array(10, "문자열", false);

document.write((typeof arr) + "<br>");    // object

document.write((typeof arr[0]) + "<br>"); // number

document.write((typeof arr[1]) + "<br>"); // string

document.write(typeof arr[2]);            // boolean
```

_*자바스크립트에서는 배열이라는 타입(type)을 별도로 제공하지 않습니다.<br/> 자바스크립트 배열은 객체(object) 타입이 되며, typeof 연산자를 사용하면 'object'를 반환합니다._

### Array객체의 메소드

| 메소드 | 설명 | 비고 |
|:---:|:---:|:---:|
| Array.isArray() | 전달받은 값이 Array 객체인지 아닌지를 검사합니다 |
| Array.from() | 다음 객체들을 배열처럼 변환시켜 줍니다. | ECMAScript 6부터 추가됨. |
| Array.of() | 인수의 수나 타입에 상관없이 인수로 전달받은 값을 가지고 새로운 Array 인스턴스를 생성합니다.| ECMAScript 6부터 추가됨.|

#### Array.isArray() 예제
```javascript
Array.isArray([]);          // true

Array.isArray(new Array()); // true

Array.isArray(123);         // false

Array.isArray("Array");     // false

Array.isArray(true);        // false
```

#### Array.from() 예제
```javascript
function arrayFrom() {
    return Array.from(arguments);
}

Array.from(arrayFrom(1, 2, 3));        // [1, 2, 3]

var myMap = new Map([[1, 2], [3, 4]]);

Array.from(myMap);                     // [1, 2, 3, 4]

Array.from("JavaScript");              // [J,a,v,a,S,c,r,i,p,t]
```

#### Array.of() 예제
```javascript
new Array(10); // [,,,,,,,,,] -> 10개의 배열 요소를 가지는 빈 배열을 생성함.

Array.of(10);  // [10] -> 한 개(숫자 10)의 배열 요소를 가지는 배열을 생성함.
```

<br/>

## 5 - 7) 다차원배열

다차원 배열이란 배열 요소가 또 다른 배열인 배열을 의미합니다.

- 지금까지 우리가 살펴본 배열은 1차원 배열입니다.
- 2차원 배열이란 배열 요소가 1차원 배열인 배열을 의미합니다. 
- 3차원 배열이란 배열 요소가 2차원 배열인 배열을 의미합니다.

즉, 배열안에 배열이 있는 형태입니다.

```javascript
var arr = new Array(3);      // 3개의 요소를 가지는 배열을 생성함.

for (var row = 0; row < 3; row++) {
    arr[row] = new Array(4); // 각각의 요소마다 또다시 4개의 요소를 가지는 배열을 생성함.
    for (var column = 0; column < 4; column++) {
        arr[row][column] = "[" + row + "," + column + "]"; // 각각의 배열 요소를 생성함.
        document.write(arr[row][column] + " ");            // 각 배열 요소에 접근함.
    }
}
```

***
