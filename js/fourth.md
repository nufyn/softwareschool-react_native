# 4장. 제어문에 대해 알아보자

***

## 4 - 1) 제어문

프로그램의 순차적인 흐름을 제어해야 할 때 사용하는 실행문을 제어문이라고 합니다.
이러한 제어문에는 조건문, 반복문 등이 포함됩니다.

<br/>

## 4 - 2) 조건문

조건문이란 프로그램 내에서 주어진 표현식의 결과에 따라 별도의 명령을 수행하도록 제어하는 실행문입니다.
조건문 중에서 가장 기본이 되는 실행문은 if 문입니다.

자바스크립트에서 사용할 수 있는 조건문의 형태는 다음과 같습니다.

1. if문
2. if / else문
3. else if문
4. switch문

### if 문

if 문은 표현식의 결과가 참(true)이면 주어진 실행문을 실행하며, 거짓(false)이면 아무것도 실행하지 않습니다.

#### 예시

```javascript
var X = 1;

if (X > 0) {
    console.log(X);
}
```

#### 퀴즈) 잘못된 곳을 찾으시오

```javascript
if (x = y) {
    document.write("두 변수 x와 y는 같습니다.");
}
```

_*위의 예제는 변수 x와 y의 값이 같으면 두 변수가 같다는 문자열을 출력하려고 하는 예제입니다.
하지만 if 문의 표현식에서 동등 연산자(==)를 사용해야 할 곳에 잘못해서 대입 연산자(=)을 사용했습니다._

### else 문

if 문과 같이 사용할 수 있는 else 문은 if 문의 표현식 결과가 거짓(false)일 때 주어진 실행문을 실행합니다.

#### 예문

```javascript
var X = -1;

if (X > 0) {
    console.log(X + "는 0보다 큽니다.");
} else {
    console.log(X + "는 0보다 작거나 같습니다.");
}
```

### else if문

else if 문은 if 문처럼 표현식을 설정할 수 있으므로, 중첩된 if 문을 좀 더 간결하게 표현할 수 있습니다.
하나의 조건문 안에서 if 문과 else 문은 단 한 번만 사용될 수 있습니다.
하지만 else if 문은 여러 번 사용되어 다양한 조건을 설정할 수 있습니다.

```javascript
var X = 0;

if (X > 0) {
    console.log(X + "는 0보다 큽니다.");
} else if(X < 0) {
    console.log(X + "는 0보다 작습니다.");
} else {
    console.log(X + "는 0과 같습니다.");
}
```

### switch 문

```javascript 
var x = 10;

switch (typeof x) {
    case "number":
        document.write("변수 x의 타입은 숫자입니다.");
        break;
    case "string":
        document.write("변수 x의 타입은 문자열입니다.");
        break;
    case "object":
        document.write("변수 x의 타입은 객체입니다.");
        break;
    default:
        document.write("변수 x의 타입을 잘 모르겠네요...");
        break;
}
```

#### 퀴즈) 오늘이 무슨 요일인지 맞추시오

```javascript
var day = new Date().getDay(); // 오늘의 요일을 반환함. (일요일: 0 ~ 토요일: 6)

switch (day) {
    case 1: // 월요일인 경우
    
    case 2: // 화요일인 경우
    
    case 3: // 수요일인 경우

    case 4: // 목요일인 경우

    default: // 0부터 6까지의 값이 아닌 경우
        document.write("아직도 주말은 멀었네요... 힘내자구요!!");
        break;
    case 5: // 금요일인 경우
        document.write("오늘은 불금이네요!!");
        break;
    case 6: // 토요일인 경우

    case 0: // 일요일인 경우
        document.write("즐거운 주말에도 열심히 공부하는 당신~ 최고에요!!");
        break;
}
```

## 4 - 3) 반복문

프로그램이 처리하는 대부분의 코드는 반복적인 형태가 많으므로, 가장 많이 사용되는 실행문 중 하나입니다.

<ol>
    <li>while문</li>
    <li>for 문</li>
</ol>

### while 문

while 문은 우선 표현식이 참(true)인지를 판단하여 참이면 내부의 실행문을 실행합니다.
내부의 실행문을 전부 실행하고 나면, 다시 표현식으로 돌아와 또 한 번 표현식이 참인지를 판단하게 됩니다.
__이렇게 표현식의 검사를 통해 반복해서 실행되는 반복문을 루프(loop)라고 합니다.__

<blockquote>
while 문 내부에 표현식의 결과를 변경하는 실행문이 존재하지 않을 경우 프로그램은 루프를 영원히 반복하게 됩니다.

이것을 무한 루프(infinite loop)에 빠졌다고 하며, 무한 루프에 빠진 프로그램은 영원히 종료되지 않습니다.

무한 루프는 특별히 의도한 경우가 아니라면 반드시 피해야 하는 상황입니다. 따라서 while 문을 작성할 때는 표현식의 결과가 어느 순간에는 거짓(false)을 갖도록 표현식를 변경하는 실행문을 반드시 포함해야 합니다.
</blockquote>

### for 문

```javascript
for (var i = 1; i < 10; i++) {
    document.write(i + "<br>");
}
```

### for / in 문

for / in 문은 해당 객체의 모든 열거할 수 있는 프로퍼티(enumerable properties)를 순회할 수 있도록 해줍니다.

### 같은 기능을 하는 단순 for문과 for / in문
```javascript
var arr = [3, 4, 5];

for (var i = 0; i < arr.length; i++) { // 배열 arr의 모든 요소의 인덱스(index)를 출력함.
    document.write(i + " ");
}

for (var i in arr) { // 위와 같은 동작을 하는 for / in 문
    document.write(i + " ");
}
```
_*for / in 문은 해당 객체가 가진 모든 프로퍼티를 반환하는 것이 아닌, 오직 열거할 수 있는 프로퍼티만을 반환합니다._

### continue 문

continue 문은 루프 내에서 사용하여 해당 루프의 나머지 부분을 건너뛰고, 바로 다음 표현식의 판단으로 넘어가게 합니다.

__보통 반복문 내에서 특정 조건에 대한 처리를 제외하고자 할 때 자주 사용됩니다.__

#### 예시 
```javascript
var exceptNum = 3;

for (var i = 0; i <= 100; i++) {
    if (i % exceptNum == 0) // exceptNum의 배수는 출력하지 않음.
        continue;
    document.write(i + " ");
}
```

### break 문

break 문은 루프 내에서 사용하여 해당 반복문을 완전히 종료시키고, 반복문 바로 다음에 위치한 실행문으로 프로그램의 흐름을 이동시킵니다.

__즉, 루프 내에서 표현식의 판단 결과에 상관없이 반복문을 완전히 빠져나가고 싶을 때 사용합니다.__

```javascript
var lectures = ["html", "css", "자바스크립트", "php"];

var topic = "자바스크립트";

for (var i = 0; i < lectures.length; i++) {

    if (lectures[i] == topic) {

        document.write(topic + " 과목은 " + (i + 1) + "번째 과목입니다.");

        break; // 원하는 값을 찾은 후에는 더 이상 for 문을 반복하지 않고 빠져나감.

    }

}
```

***
