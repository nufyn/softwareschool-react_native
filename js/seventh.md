# 7장. 객체(Object)

***

## 7 - 1) 객체란

객체(object)란 실생활에서 우리가 인식할 수 있는 사물로 이해할 수 있습니다.
상태나 특성 등의 정보인 property와 객체 조작을 위한 method로 구분합니다.

_*첫장에서 javascripts가 객체기반의 언어라고 말했습니다. 바로 그 객체가 이 객체입니다._

객체란 이름(name)과 값(value)으로 구성된 프로퍼티(property)의 정렬되지 않은 집합입니다.
프로퍼티의 값으로 함수가 올 수도 있는데, 이러한 프로퍼티를 메소드(method)라고 합니다.

```javascript
var cat = "나비"; // 일반적인 변수의 선언

// 객체도 많은 값을 가지는 변수의 하나임.
var kitty = { name: "나비", family: "코리안 숏 헤어", age: 1, weight: 0.1 };

cat          // 나비
kitty.name   // 나비
```

>자바스크립트에서는 숫자, 문자열, 불리언, undefined 타입을 제외한 모든 것이 객체입니다.
하지만 숫자, 문자열, 불리언과 같은 원시 타입은 값이 정해진 객체로 취급되어, 객체로서의 특징도 함께 가지게 됩니다.

<br/>

## 7 - 2) 객체의 생성

객체를 생성하는 방법

1. 리터럴 표기(literal notation)를 이용한 방법
2. 생성자 함수(constructor function)를 이용한 방법
3. Object.create() 메소드를 이용한 방법

>위와 같은 방법으로 생성되어 메모리에 대입된 객체를 인스턴스(instance)라고 합니다.

### 리터럴을 이용한 방법
```javascript
var kitty = {
    name: "나비", // 프로퍼티네임은 식별자를 이용해도 되고 
    "family": "코리안 숏 헤어", //문자열을 이용해도 됨.
    age: 1,
    weight: 0.1
};

document.write("우리 집 새끼 고양이의 이름은 " + kitty.name + "이고, 종은 " + kitty.family + "입니다.");
```

### new 연산자(생성자)를 이용한 방법

객체를 생성하고 초기화할 수 있는 메소드를 생성자(constructor)라고 합니다.

자바스크립트는 원시 타입을 위한 생성자를 미리 정의하여 제공합니다.
```javascript
var day = new Date(); // new 연산자를 사용하여 Date 타입의 객체를 생성함.

document.write("올해는 " + day.getFullYear() + "년입니다.");
```

### 객체생성 메소드를 이용하는 방법

Object.create() 메소드는 지정된 프로토타입(prototype) 객체와 프로퍼티를 가지고 새로운 객체를 만들어 줍니다.

따라서 이 메소드를 이용하면 사용자가 프로토타입 객체를 직접 명시할 수 있으므로, 상당히 유용하게 사용됩니다.

```javascript
var obj = Object.create(null, {             // null 프로토타입을 사용하여 새로운 객체를 만들고
    x: { value: 100, enumerable: true },    // x좌표를 나타내는 열거할 수 있는 프로퍼티와
    y: { value: 200, enumerable: true }     // y좌표를 나타내는 열거할 수 있는 프로퍼티를 추가함.
});

obj.x;                      // x좌표

obj.y;                      // y좌표 

Object.getPrototypeOf(obj); // 객체의 프로토타입을 반환해 줌.
```

<br/>

## 7 - 3) 객체의 참조

### 객체의 프로퍼티 참조
```javascript
var person = {
    name: "홍길동",      // 이름 프로퍼티를 정의함.
    birthday: "030219",  // 생년월일 프로퍼티를 정의함.
    pId: "1234567",      // 개인 id 프로퍼티를 정의함.

    fullId: function() { // 생년월일과 개인 id를 합쳐서 주민등록번호를 반환함.
        return this.birthday + this.pId;
    }
};

person.name    // 홍길동

person["name"] // 홍길동
```

### 객체의 메소드 참조
```javascript
var person = {
    name: "홍길동",
    birthday: "030219",
    pId: "1234567",

    fullId: function() {
        return this.birthday + this.pId;
    }
};

person.fullId() // 0302191234567

person.fullId;  // function () { return this.birthday + this.pId; } 
```
_*메소드를 참조할 때 메소드 이름 뒤에 괄호()를 붙이지 않으면, 메소드가 아닌 프로퍼티 그 자체를 참조하게 됩니다.
따라서 괄호를 사용하지 않고 프로퍼티 그 자체를 참조하게 되면 해당 메소드의 정의 그 자체가 반환됩니다._

## 7 - 4) 자바스크립트에서의 객체

###  프로토타입(prototype)

자바스크립트의 모든 객체는 프로토타입(prototype)이라는 객체를 가지고 있습니다.

모든 객체는 그들의 프로토타입으로부터 프로퍼티와 메소드를 상속받습니다.

이처럼 자바스크립트의 모든 객체는 최소한 하나 이상의 다른 객체로부터 상속을 받으며, 이때 상속되는 정보를 제공하는 객체를 프로토타입(prototype)이라고 합니다.

### 상속(inheritance)
상속(inheritance)이란 새로운 클래스에서 기존 클래스의 모든 프로퍼티와 메소드를 사용할 수 있는 것을 의미합니다.

 

상속을 통해 새로운 프로그램의 요구에 맞게 기존 클래스를 수정하여 재사용할 수 있습니다.

또한, 클래스 간의 종속 관계를 형성함으로써 객체의 관계를 조직화할 수 있는 장점이 있습니다.

따라서 이러한 상속은 추상화, 캡슐화와 더불어 객체 지향 프로그래밍을 구성하는 중요한 특징 중 하나가 됩니다.

 

하지만 C#이나 C++과 같은 클래스 기반(class-based)의 객체 지향 언어와는 달리 자바스크립트는 프로토타입 기반(prototype-based)의 객체 지향 언어입니다.

프로토타입 기반이기 때문에 상속의 개념이 클래스 기반의 객체 지향 언어와는 약간 다릅니다.

자바스크립트에서는 현재 존재하고 있는 객체를 프로토타입으로 사용하여, 해당 객체를 복제하여 재사용하는 것을 상속이라고 합니다.

***
