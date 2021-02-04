---
layout: post
title: "[TIL/Javascript] 자바스크립트의 연산자, switch문, 엄격 모드"
date: 2020-01-26 23:52:23 +0900
category: Javascript
comments: true
---

## 1. 기본 연산자와 수학

* 피연산자(operand) : 연산자가 연산을 수행하는 대상
* 단항(unary) 연산자 : 피연산자를 하나만 받는 연산자
* 이항(binary) 연산자 : 피연산자 두 개를 받는 연산자

```
x = -x;	// 단항 연산자 -
y = y - x; // 이항 연산자 -
```

### 수학 연산자

* 덧셈 연산자 `+`
* 뺄셈 연산자 `-`
* 곱셈 연산자 `*`
* 나눗셈 연산자 `/`
* 나머지 연산자 `%`
* 거듭제곱 연산자 `**`

#### 이항 연산자 '+' 와 문자열 연결

* 피연산자 중 하나가 문자열이면 다른 하나도 문자열로 변환됨

```javascript
let s = "my"+"string";
alert(s);		// mystring
alert('1'+2);	// "12"
alert(2+2+'1');	// '41'
```

#### 단항 연산자 `+`
* 피연산자가 숫자가 아닌 경우 숫자형으로 변환

```javascript
alert( +true );	// 1
alert( +"" );	// 0
```

#### 연산자 우선순위
* 하나의 표현식에 둘 이상의 연산자가 있는 경우, 실행 순서는 연산자의 우선순위(precedence)에 의해 결정

#### 할당 연산자 `=`
* 우항의 결과가 좌항에 할당됨
* 할당 연산자 체이닝 : 여러 개를 연결할 수 있음

```javascript
let c = 3 - (a = b + 1);
alert(c);			// 0
a = b = c = 2 + 2;		
alert(c);			// 4
```

#### 복합 할당 연산자
* 수학 연산자와 할당 연산자의 조합

```javascript
let n = 2;
n += 5;	// 7
n *= 2;	// 14
```

#### 증가/감소 연산자
* 증가 연산자 `++` : 변수를 1 증가
* 감소 연산자 `--` : 변수를 1 감소
* 전위형/후위형으로 구분
  * 전위형 : 피연산자 앞에 올 때, 변수를 증감시키고 변환
  * 후위형 : 피연산자 뒤에 올 때, 변수를 변환하고 증감시킴

#### 비트 연산자 (bitwise operator)
인수를 32비트 정수로 변환하여 이진 연산을 수행
* 비트 AND `&`
* 비트 OR `|`
* 비트 XOR `^`
* 비트 NOT `~`
* 왼쪽 시프트 LEFT SHIFT `<<`
* 오른쪽 시프트 RIGHT SHIFT `>>`
* 부호 없는 오른쪽 시프트 ZERO-FILL RIGHT SHIFT `>>>`

#### 쉼표 연산자 (comma operator)
* 마지막 표현식의 평과 결과만 반환됨

```javascript
let a = (1 + 2, 3 + 4);
alert(a);		// 7
```

## 2. switch문
여러 개의 if 조건문을 switch문으로 바꿀 수 있다.

```javascript
switch(x) {
	case 'value1' :
	...
	[break]

	case 'value2' :
	...
	[break]

	default :
	...
	[break]
}
```

* 변수 x와 'value1'을 비교 -> 일치 시 실행
-> 변수 x와 'value2'를 비교 -> 일치 시 실행
...
-> default문 아래의 코드가 실행
* default문이 필수는 아니다.
* case문 안에 break문이 없으면 조건에 부합하는지 여부를 따지지 않고 이어지는 case문을 실행한다.
* case문의 인수('value1', 'value2')에는 어떤 표현식이든 올 수 있다.
* 비교하려는 값과 case문의 값의 형과 값이 같아야 해당 case문이 실행된다.

#### 여러 개의 "case"문 묶기

```javascript
switch (a) {
	...
	case 3:
	case 5:
		alert('계산이 틀립니다!');
	...
}

```

* `case 3`과 `case 5`는 동일한 메세지를 보여준다.

 

 

### 엄격 모드
#### use strict
* 스크립트 최상단에 위치해야 한다.
* ES5에서 변경된 사항이 활성화되게 해놓는다.
* 코드를 클래스와 모듈을 사용해 구성한다면 생각해도 된다.
#### 브라우저 콘솔을 사용하는 경우
* `use strict`를 입력한 후 `Shift+Enter키`를 눌러서 줄바꿈 후 원하는 스크립트 입력




참고 : https://ko.javascript.info/