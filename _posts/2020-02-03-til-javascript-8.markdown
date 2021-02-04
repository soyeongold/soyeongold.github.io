---
layout: post
title: "[TIL/Javascript] 자바스크립트의 화살표함수, 사용자 인터페이스 기능"
date: 2020-02-03 23:52:23 +0900
category: Javascript
comments: true
---


## 화살표 함수

함수 표현식보다 단순하고 간결한 문법으로 함수를 만들 수 있는 방법

```javascript
let func = (arg1, arg2, ...argN) => expression

/* 위와 동일한 코드 (함수 표현식)
let func = function(arg1, arg2, ...argN) {
return expression;
};
*/`
```

* 함수 `func`는 인자 `arg1, arg2 ... argN`을 받고, 화살표 `=>` 우측의 `표현식(expression)`을 평가한 후에 평가 결과를 반환한다.
* 인수가 하나밖에 없다면 인수를 감싸는 괄호를 생략할 수 있다.
* 인수가 하나도 없을 땐 괄호를 비워놓으면 된다. (괄호 생략 불가)

```javascript
let double = n => n * 2;
let sayHi = () => alert("Hello");
```

#### 동적으로 사용하는 경우

```javascript
let welcome = (age < 18) ?
() => alert("안녕");
() => alert("안녕하세요");
```
#### 본문이 여러 줄인 경우

* 본문을 중괄호 안에 넣어주어야 한다.
* `return`지시자를 사용해 명시적으로 결과값을 반환해 주어야 한다.

```javascript
let sum = (a, b) => {
let result = a + b;
return result;
}
```


## 최소한의 사용자 인터페이스 기능 (alert, prompt, confirm)

### alert

```javascript
alert("message");
```

사용자가 `확인(OK)` 버튼을 누를 때까지 메시지를 보여주는 모달 창을 띄워준다.
* 모달 창(modal window) : 페이지의 나머지 부분과 상호작용이 불가능하다. (확인 버튼을 누르기 전까지 모달 창 바깥 부분을 누를 수 없다.)


### prompt

```javascript
result = prompt(title, [default]);
```

텍스트 메시지와 `입력 필드(input filed)`, `확인(OK)` 및 `취소(Cancel)` 버튼이 있는 모달 창을 띄워준다.
* `title` : 사용자에게 보여줄 문자열
* `default` : 입력 필드의 초기값
  * `[..]` : 선택값인 매개변수


### confirm

```javascript
result = confirm(question);
```

매개변수로 받은 `질문(question)`과 `확인` 및 `취소` 버튼이 있는 모달 창을 띄워준다.
사용자가 확인버튼을 누르면 `true`, 그 외의 경우는 `false`를 반환한다.
