---
layout: post
title: "[TIL/Javascript] 자바스크립트의 객체, 메서드, this"
date: 2020-02-04 23:52:23 +0900
category: Javascript
comments: true
---

## 객체

### 객체 생성 방법

* `객체 생성자` 문법
* `객체 리터럴` 문법 (주로 이 방법을 사용)

```javascript
let user = new Object();// `객체 생성자` 문법
let user = {};// `객체 리터럴` 문법
```


### 리터럴과 프로퍼티

* 중괄호 `{...}` 안에는 `키:값` 쌍으로 구성된 프로퍼티가 들어간다.
* `키`에는 문자형, `값`에는 모든 자료형 허용한다.
* 객체에서는 키를 이용하여 프로퍼티를 쉽게 찾을 수 있다.
* 프로퍼티 `키`는 프로퍼티 `이름` 혹은 `식별자`라고도 부른다.
* 여러 단어를 조합해 프로퍼티 이름을 만든 경우엔 프로퍼티 이름을 `따옴표`로 묶어줘야 한다.

```javascript
let user = {// 객체
name : "John",// 키 : "name", 값 : "John"
age : 30// 키 : "age", 값 : 30
"likes birds" : true// 키 : "likes birds", 값 : true
};
```

#### 프로퍼티 값 접근/추가
* 점 표기법(dot notation) 이용
  * 키가 '유효한 변수 식별자'인 경우 (공백 X, 숫자로 시작 X, $과 _를 제외한 특수문자 X)

```javascript
alert(user.name);// John
alert(user.age);// 30
user.isAdmin = true;// user 객체에 프로퍼티 추가
```

* 대괄호 표기법(square bracket notation) 사용
  * 키가 `유효한 변수 식별자`가 아닌 경우

```javascript
let user = {};
// 값 접근(set)
user["likes birds"] = true;
// 값 얻기(get)
alert(user["likes birds"]);// true
// 값 삭제(delete)
delete user["likes birds"];
```

#### 프로퍼티 삭제

* `delete` 연산자 사용
```javascript
delete user.age;
```

#### 계산된 프로퍼티 (computed property)

* 객체를 만들 때 객체 리터럴 안의 프로퍼티 키가 대괄호로 둘러싸여 있는 경우 (객체 생성 시 대괄호 표기법 사용)
* 프로퍼티 이름을 변수에서 가져올 때 사용

```javascript
let fruit = prompt("어떤 과일을 구매하시겠습니까", "apple");

let bag = {
[fruit] : 5,// 변수 fruit에서 프로퍼티 이름을 동적으로 받아온다. (bag.apple = 5)
[fruit + "Computers"] : 7,// 복잡한 표현식 가능 (bag.appleComputers = 7)
};

alert(bag.apple);// 변수 fruit에 "apple"이 할당되었다면 프로퍼티 이름이 "apple"이 되어, 5가 출력된다.
```

#### 단축 프로퍼티

* 프로퍼티들의 이름과 값이 변수의 이름과 동일할 경우
* 프로퍼티 값 단축 구문(property value shorthand)

```javascript
function makeUser(name, age) {
return {
name,// name: name과 같다.
age,// age: age와 같다.
};
}

let user = makeUser("John", 30);
}
```

#### 프로퍼티 이름의 제약사항

* 어떤 문자형, 심볼형 값도 프로퍼티 키가 될 수 있다. (for, let, return 같은 예약어 사용 가능)
* 문자형이나 심볼형에 속하지 않은 값은 문자열로 자동 형 변환된다.


### `in` 연산자로 프로퍼티 존재 여부 확인하기

* 해당 key를 가진 프로퍼티가 객체 내에 있는지 확인

```javascript
"key" in object
```

* 자바스크립트는 존재하지 않는 프로퍼티에 접근하려 해도 에러가 발생하지 않고 `undefined` 반환
  * `undefined`와 비교하여 프로퍼티 존재 여부 확인 가능하다.
  * 변수는 정의되어 있으나 값이 할당되지 않은 경우/값이 undefined일 경우에 실패할 수 있다.

```javascript
let user = {
name : undefined,
age : 30;
}
alert("age" in user);// true
alert("name" in user);// true
alert(user.name === undefined);// true (프로퍼티가 존재하는데, 값이 undefined이므로 존재하지 않는다고 나타남)
```


### 'for...in'으로 객체의 모든 키를 순회

```javascript
for (key in object) {
// 각 프로퍼티 키(key)를 이용하여 본문(body)를 실행한다.
}
```
* `for...in` 반복문 안에서 반복 변수(looping variable)을 선언(`let key`)할 수 있다.

```javascript
let user = {
name : "Soyeon",
age : 24
};
for (let key in user) {
alert(key);// name, age
alert(user[key]);// Soyeon, 24
}
```

### 객체 정렬 방식

* 정수 프로퍼티(integer property)는 자동으로 정렬
  * 정수 프로퍼티 : 변형 없이 정수에서 왔다 갔다 할 수 있는 문자열 (숫자만 있는 문자열)
* 그 외의 프로퍼티는 객체에 추가한 순서 그대로 정렬

```javascript
let codes = {
"49" : "독일",
"41" : "스위스",
// ...
"1" : "미국"
};
for (let code in codes) {
alert(code);// 1, ... 41, 49
}
```

## 메서드 (method)
* 객체 프로퍼티에 할당된 함수
* 객체에게 행동할 수 있는 능력을 부여해주기 위하여 객체의 프로퍼티에 함수를 할당

### 메서드 만들기

* 함수 표현식으로 함수를 만들고, 객체 프로퍼티에 함수를 할당

```javascript
let user = {
name : "Soyeon",
age : 24
};

user.sayHi = function() {
alert("안녕");
};
```

* 이미 정의된 함수를 이용해서 메서드로 등록 (별개의 객체에서 동일한 함수를 사용할 수 있음)

```javascript
let user = {
// ...
};

// 함수 선언
function sayHi() {
alert("안녕");
};

// 선언된 함수를 메서드로 등록
user.sayHi = sayHi;
```

* 객체 리터럴 안에 메서드 선언하는 두 가지 방법

```javascript
let user = {
// ...
sayHi : function() {
alert("안녕");
}
};
```

```javascript
let user = {
// ..
sayHi() {
alert("안녕");
}
};
```

## this

* `this`는 *메서드를 호출할 때 사용된 객체*를 나타낸다. (this가 있는 함수가 호출될 때의 객체)
* 메서드 내부에서 `this` 키워드를 사용하면 객체에 접근할 수 있다.
* `this`를 사용하지 않고 외부 변수를 참조하여 객체에 접근할 수 있다.
  * 예상치 못한 에러가 발생할 수 있다. (참조한 외부 변수를 다른 값(null)으로 덮어썼을 경우)

```javascript
let user = {
name : "Soyeon",
age : 24,

sayHi() {
alert(this.name);
}
};

user.sayHi();// Soyeon
```

* `this`의 값은 호출하는 객체에 따라 달라진다. (런타임에 결정됨)
  * 함수가 호출되기 전까지 `this`에 값이 할당되지 않는다.

```javascript
let user = { name : "Soyeon" };
let admin = { name : "Admin" };

function sayHi() {
alert(this.name);
}

// 별개의 객체에서 동일한 함수를 사용
user.f = sayHi;
admin.f = sayHi;

user.f();// Soyeon (this == user)
admin.f();// Admin (this == admin)
```

### 'this'가 없는 화살표 함수

* 화살표 함수는 자신만의 `this`를 가지지 않는다.
  * 화살표 함수 안에서 `this`를 사용하면, 외부에서 `this` 값을 가져온다.

```javascript
let user = {
name : "Soyeon",
sayHi() {
let arrow = () => alert(this.name);
arrow();
}
};

user.sayHi();// Soyeon ( arrow()의 this는 외부 함수 user.sayHi()의 this가 된다 )
```

## 참조에 의한(by reference) 객체 복사

* 객체가 할당된 변수를 복사할 땐 객체의 참조값이 복사되고 객체는 복사되지 않는다.
  * 여러 변수를 사용하여 객체에 접근하거나 객체를 조작할 수 있다.

```javascript
let user = {name : 'Soyeon'};
let admin = user;

admin.name = 'Kimsoyeon';// 'admin'참조 값에 의해 변경됨
alert(user.name);// Kimsoyeon
```


### 참조에 의한 비교

* 객체 비교 시 동등 연산자 `==`와 일치 연산자 `===`는 동일하게 동작 (객체 비교 시에는 참조값으로 비교하는 듯 하다)
  * 피연산자인 두 객체게 동일한 객체인 경우에 참을 반환
* 원시값과의 비교 시 객체가 원시형으로 변환


### 객체 복사, 병합

* 새로운 객체를 만든 다음 기존 객체의 프로퍼티들을 순회해 원시 수준까지 프로퍼티를 복사

```javascript
let user = {
  name : "Soyeon",
  age : 24
};

let clone = {};// 새로운 빈 객체

for (let key in user) {// 빈 객체에 user 프로퍼티 전부를 복사해 넣는다.
  clone[key] = user[key];
}
```

* `Object.assign` 사용 (복사/병합)

```
Object.assign(dest, [src1, src2, src3 ...])
```
* `dest` : 목표로 하는 객체
* `src1, src2...` : 복사하고자 하는 객체 (필요에 따라 여러가지 많은 객체를 인수로 사용 가능)
* 동작 방식 : `src1, src2...`의 프로퍼티를 `dest`에 복사 후 `dest`를 반환
* 목표 객체에 동일한 이름을 가진 프로퍼티가 있는 경우엔 기존 값이 덮어씌워져 새로운 값으로 바뀐다.


### 중첩 객체 복사

* 깊은 복사(deep cloning) 사용
  * 중첩 객체 복사의 문제 : 프로퍼티 중 다른 객체에 대한 참조값일 경우 프로퍼티를 복사하는 것만으로는 복제할 수 없다. (참조값이 복사되기 때문)
  * 프로퍼티 키의 각 값을 검사하면서, 그 값이 객체인 경우 객체의 구조도 복사해주는 반복문 사용
  * 자바스크립트 라이브러리 'loadash'의 메서드인 `_.cloneDeep(obj)`를 사용하면 처리 가능


## 생성자 함수

유사한 객체 여러 개를 생성할 때 사용
* 관례
  1. 함수 이름의 첫 글자는 대문자로 시작한다.
  2. 반드시 `"new"` 연산자를 붙여 실행한다.
* 알고리즘
  1. 빈 객체를 만들어 `this`에 할당한다.
  2. 함수 본문을 실행한다. `this`에 새로운 프로퍼티를 추가하여 `this`를 수정한다.
  3. `this`를 반환한다.

```javascript
function User(name) {
  // this = {};(빈 객체가 암시적으로 만들어짐)
  this.name = name;// 새로운 프로퍼티를 this에 추가함
  this.isAdmin = false;
  // return this;(this가 암시적으로 반환됨)
}

let user = new User("Soyeon");

alert(user.name);// Soyeon
```

### 재사용할 필요가 없는 복잡한 객체를 생성할 때 : 익명 생성자 함수 사용

* 재사용을 막으면서 코드를 캡슐화할 수 있다.

```javascript
let user = new function() {
  this.name = "Soyeon";
  this.isAdmin = false;
  // 복잡한 객체를 만들기 위한 코드들이 여기에 들어간다.
};
```


### new.target

* `new.target` 프로퍼티를 사용하면 함수가 `new`와 함께 호출되었는지 아닌지 알 수 있다.
  * `new`와 함께 호출한 경우 `함수 자체`를 반환
  * 일반적인 방법으로 호출한 경우 `undefined`를 반환

```javascript
function User() {
  alert(new.target);
}

User();// undefined

new User();// function User {...}
```

### 생성자와 return문 (특이 케이스)

* 객체를 return한다면, this대신 `객체`가 반환
* 원시형을 return한다면, return문이 무시


### 생성자 내 메서드

* 생성자 함수를 통해 `this`에 메서드를 더해줄 수 있다. (class 문법을 사용한 것과 마찬가지)

```javascript
function User(name) {
  this.name = name;
  this.sayHi = function() {
    alert("내 이름은 " + this.name);
};

let soyeon = new User("소연");
john.sayHi();// 내 이름은 소연
```
