---
layout: post
title: "[TIL/Javascript] 자바스크립트의 변수와 상수, 조건 처리"
date: 2020-01-28 23:52:23 +0900
category: Javascript
comments: true
---

## 1. 변수 (variable)

데이터를 저장할 때 쓰이는 '이름이 붙은 저장소'
* 변수 선언 : `let` 키워드 사용하여 변수 생성
* 변수에 데이터 저장 : 할당 연산자 `=` 사용
* 변수 접근 : 변수명을 이용

```javascript
let message;		// message 변수 생성
message = 'Hello';		// 문자열 저장

alert(message);		// message 변수에 접근하여 변수에 저장된 값을 보여준다.
```

* 변수 선언과 값 할당을 한 줄에 작성할 수 있다.
* 한 줄에 여러 변수를 선언할 수 있다. (권장 X)
* `var` 키워드는 `let`처럼 변수를 선언하는데 사용, 다만 오래된 방식이다.
* 변수를 두 번 선언하면 에러가 발생한다.


### 변수를 정의하는 여러가지 방법
* 가독성을 위해 한 줄에 하나의 변수 선언
```javascript
let user = 'John';
let age = 25;
let message = 'Hello';
```

```javascript
let user = 'John'
  , age = 25
  , message = 'Hello';
```


### 변수 명명 규칙

1. 변수명에는 오직 문자와 숫자, 그리고 기호 `$`과 `_`만 들어갈 수 있다.
2. 첫 글자는 숫자가 될 수 없다.
* 대소문자가 구별된다.
* 예약어는 변수명으로 사용할 수 없다.

 

### 카멜 표기법 (camelCase)

* 여러 단어를 조합하여 변수명을 만들 때 흔히 사용한다.
* 단어를 차례대로 나열하면서 첫 단어를 제외한 각 단어의 첫 글자를 대문자로 작성한다.
  * 예) myVeryLongName



## 2. 상수 (constant)

변화하지 않는 변수
* 상수 선언 : `const` 키워드를 사용하여 상수 생성
* 상수는 재할당할 수 없으므로 상수를 변경하려고 하면 에러가 발생한다.
* 대부분 대문자와 밑줄로 구성된 이름으로 정한다.
  * 예) COLOR_RED



## 3. 조건 처리

`if`문과 조건부 연산자 `?` 사용


### `if`문

* `if(...)`문은 괄호 안에 들어가는 조건을 평가하여, 그 결과가 `true`이면 코드 블록 실행
* 중괄호 `{}`를 사용하여 코드를 블록으로 감싸는 것을 추천 (코드 가독성 증가)

```javascript
if (year = 2021) {
	alert("안녕하세요!");
	alert("2021년 새해 복 많이 받으세요!");
}
```


### `else`절

* `if`문 뒤에 `else`절을 붙일 수 있다.
* 평가한 조건이 `false`일 때 실행된다.

```javascript
if (year = 2021) {
	alert("2021년 행복하세요!");
} else {
	alert("안녕하세요!");		// year가 2021 이외의 값인 경우 실행된다.
}
```


#### `else if` 복수 조건 처리하기

* 여러 개의 조건을 처리해야할 때 `else if`를 사용할 수 있다.
* 마지막에 붙는 `else`는 선택 사항이다.

```javascript
if (year < 2021) {
	alert("숫자를 더 올려보세요!");
} else if (year > 2021) {
	alert("숫자를 더 내려보세요!");
} else {
	alert("정답입니다");
}
```

 

### 조건부(conditional) 연산자 `?`

* 조건에 따라 변수에 다른 값을 할당할 때 사용
* 삼항(ternary) 연산자 : 피연산자가 세 개이기 때문
* `condition`이 truthy라면 `value1`이, 그렇지 않다면 `value2`가 반환됨

```javascript
let result = condition ? value1 : value2;
```



참고 : https://ko.javascript.info/