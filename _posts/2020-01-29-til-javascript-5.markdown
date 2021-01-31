---
layout: post
title: "[TIL/Javascript] 자바스크립트의 함수표현식과 콜백함수"
date: 2020-01-29 23:52:23 +0900
category: Javascript
comments: true
---

## 1. 함수 표현식 (Function Expression)

* 자바스크립트는 함수를 특별한 종류의 값으로 취급한다. 

```javascript
let sayHi = function() {
	alert("Hello");
};			// 함수 표현식이 값처럼 취급되어 변수에 할당되므로 세미콜론을 붙이는 게 좋다.

```

  * 함수 코드를 문자형으로 바꾸어 출력할 수 있다.
  
```javascript
function sayHi() {
	alert("Hello");
}

alert(sayHi);	// 함수 코드가 보인다.
```

  * 함수를 복사하여 다른 변수에 할당할 수도 있다.

```javascript
function sayHi() {		// 함수 생성
	alert("Hello");
}

let func = sayHi;		// 함수를 변수에 복사
func();			// 복사한 함수를 실행
sayHi();			// 본래 함수도 정상적으로 실행 가능
```

 

## 2. 콜백 함수

함수가 함수의 인수로 전달되어, 인수로 전달된 그 함수는 나중에 호출(called back)될 수 있다.
* `question` : 질문
* `yes` : "Yes"라고 답한 경우 실행되는 함수
* `no` : "No"라고 답한 경우 실행되는 함수
사용자가 "yes"라고 대답한 경우 `showOk` 가 콜백이 되고, "no"라고 대답한 경우 `showCancel`이 콜백이 된다.

```javascript
function ask(question, yes, no) {
	if (confirm(question)) yes()
	else no();
}

function showOk() {
	alert("동의하셨습니다.");
}

function showCancel() {
	alert("취소하셨습니다.");
}

// 함수 showOk와 showCancel이 ask 함수의 인수로 전달되었다.
ask("동의하십니까?", showOk, showCancel);
```

* 함수 표현식을 사용한 예시 (코드 길이 단축)

```javascript
function ask(question, yes, no) {
	if (confirm(question)) yes()
	else no();
}

// ask 함수 호출, 익명 함수(anonymous function)를 인수로 전달
ask(
	"동의하십니까?",
	function() { alert("동의하셨습니다."); }, 
	function() { alert("취소하셨습니다."); } 
);
```
 

### 함수 표현식 vs 함수 선언문

#### 차이점

1. 문법
* 함수 선언문 : 주요 코드 흐름 중간에 독자적인 구문 형태로 존재
* 함수 표현식 : 표현식이나 구문 구성 내부에 생성
  
2. 자바 스크립트 엔진이 언제 함수를 생성하는지
* 함수 선언문 : 실행 전, 함수 선언문을 찾고 해당 함수를 생성한다. 따라서 함수 선언문이 정의되기 전에 호출할 수 있다.
* 함수 표현식 : 실제 실행 흐름이 해당 함수에 도달했을 때 함수를 생성한다. 따라서 실행 흐름이 함수에 도달했을 때 부터 해당 함수를 사용할 수 있다.
  
3. 스코프
* 함수 선언문 : 코드 블록 내에 위치하면 해당 함수는 블록 내 어디서든 접근할 수 있다. 하지만 블록 밖에서는 함수에 접근하지 못한다. 
* 함수 표현식 : 코드 블록 밖에 선언한 변수에 함수 표현식으로 만든 함수를 할당하여 코드 블록 밖에서 함수에 접근할 수 있다.