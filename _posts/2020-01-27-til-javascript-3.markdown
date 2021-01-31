---
layout: post
title: "[TIL/Javascript] 자바스크립트의 비교연산자, 함수"
date: 2020-01-27 23:52:23 +0900
category: Javascript
comments: true
---

## 1. 비교연산자

* 보다 큼/작음 : `a > b`, `a < b`
* 보다 크거나/작거나 같음 : `a >= b`, `a <= b`
* 같음(동등) : `a == b`
* 같지 않음(부등) : `a != b`

### 불린형 반환

* 비교 연산자는 불린형을 반환한다.
  * true 반환 : 긍정, 참, 사실
  * false 반환 : 부정, 거짓, 사실이 아님

 

### 문자열 비교

* '사전' 순으로 문자열 비교 (정확히는 유니코드 순)
* 문자열 비교 시 알고리즘
  1. 두 문자열의 첫 글자 비교한다.
  2. 첫 번째 문자열의 첫 글자가 다른 문자열의 첫 글자보다 크면(작으면), 첫 번째 문자열이 두 번째 문자열보다 크다고(작다고) 결론 내고 비교를 종료한다.
  3. 두 문자열의 첫 글자가 같으면 두 번째 글자를 같은 방식으로 비교한다.
  4. 글자 간 비교가 끝날 때까지 이 과정을 반복한다.
  5. 비교가 종료되었고 문자열의 길이도 같다면 두 문자열은 동일하다고 결론을 낸다. 비교가 종료되었지만 두 문자열의 길이가 다르면 길이가 긴 문자열이 더 크다고 결론 낸다.

```javascript
alert('Z' > 'A');	// true
alert('Glow' > 'Glee');	// true
alert('Bee' > 'Be');	// true
```

* 'Z' > 'A' : 사전에서 'Z'가 'A'보다 뒤에 있기 때문에 'Z'가 더 크다
* 'Glow' > 'Glee' : G와 l이 같고 o가 e보다 크기 때문에 'Glow'가 더 크다
* 'Bee' > 'Be' : 'Bee'가 'Be'보다 길기 때문에 'Bee'가 더 크다

 

### 다른 형을 가진 값 간의 비교
비교하려는 값의 자료형이 다를 때 값들을 *숫자형*으로 바꾼다.

```javascript
alert('2' > 1);	// true
```

 

### 일치 연산자 '==='
형 변환 없이 값을 비교할 수 있다.

```javascript
alert(0 == false);	// true, false가 0으로 변환되기 때문이다.
alert(0 === false);	// false, 피연산자의 형이 다르기 때문이다.
```

### null과 undefined 비교
```javascript
alert(null === undefined);	// false
alert(null == undefined);	// true
```

* 일치 연산자 `===`를 사용하여 비교 : 두 값의 자료형이 다르기 때문에 false
* 동등 연산자 `==`를 사용하여 비교 : `null`과 `undefined`를 비교하면 특별한 규칙이 적용되어 true
* 산술 연산자나 기타 비교 연산자 `< > <= >=`를 사용하여 비교 : 숫자형으로 변환되어 `null`은 `0`, `undefined`은 `NaN`으로 변환

### null vs 0
```javascript
alert(null > 0);	// false
alert(null == 0);	// false
alert(null >= 0);	// true
```

* `>`에서는 `null`이 `0`으로 변환되어 false
* '=='에서는 `null`이 형 변환을 하지 않아서 false (`null`이나 `undefined`를 다른 값과 비교할 때 무조건 false 반환)
* `>='에서는 `null`이 `0`으로 변환되어 true

 

### 비교가 불가능한 undefined

```javascript
alert(undefined > 0);	// false
alert(undefined < 0);	// false
alert(undefined == 0);	// false
```

* `>` `<`에서는 `undefined`가 `NaN`으로 변환되어 항상 false
* `==`에서는 `null`이나 `undefined`와 같고, 그 이외의 값과는 같지 않기 때문에 false

## 2. 함수

* 유사한 동작을 하는 코드를 여러 번 호출할 수 있다.
* 주로 중복 코드를 피하기 위해 사용한다.


### 함수 선언 (function declaration)

```javascript
function name(parameters) {
	// 함수 본문
}
```

1. `function` 키워드, 함수 이름, 괄호로 둘러싼 매개변수(parameters)를 차례로 쓴다.
2. 매개변수가 여러 개 있다면 각 매개변수를 콤마로 구분한다.
3. 함수 본문(body)를 중괄호로 감싸 붙여준다.


### 함수 호출

```javascript
function showMessage() {
	alert("안녕하세요!");
}

showMessage();	// 함수 호출
```


### 지역 변수 (local variable)

* 함수 내에서 선언한 변수
* 함수 안에서만 접근 가능

```javascript
function showMessage() {
	let message = "Hello";	// 지역 변수 선언

	alert(message);		// "Hello" 출력
}
```


### 외부 변수 (outer variable)

* 함수 외부의 변수
* 모든 함수에서 접근, 수정 가능 (함수 내부에 외부 변수와 동일한 이름을 가진 변수가 없는 경우에만)

```javascript
let userName = 'John';

function showMessage() {
	let userName = 'Soyeon';
	let message = "Hello, " + userName;	

	alert(message);		// Hello, Soyeon
}
``` 


### 매개변수 (parameter)

* 임의의 데이터를 함수 안에 전달할 수 있다.

```javascript
function showMessage(from, text) {
	alert(from + ' : ' + text);
}

show Message('Soyeon', 'Hello');	// Soyeon : Hello
```

* 함수 안에서 외부 변수의 값을 변경하여도 외부 변수에 반영되지 않는다.

```javascript
function showMessage(from, text) {
	from = '*' + from + '*';
	alert(from + " : " + text);
}

let from = "Soyeon";
showMessage(from, "Hello");		// *Soyeon* : Hello
alert(from);			// Soyeon
```


### 기본값 (default value)

* 매개변수에 값을 전달하지 않으면 그 값은 `undefined`가 된다.

```javascript
showMessage("Soyeon");		// Soyeon : undefined
```

* 매개변수에 값을 전달하지 않아도 `undefined`가 되지 않게 하려면 '기본값'을 설정해주면 된다.

```javascript
function showMessage(from, text = "no text given") {
	alert(from + " : " + text);
}

showMessage("Soyeon");		// Soyeon : no text given
```

* 이 외의 매개변수 기본값 설정 방법
  * `if문` 사용 : `undefined`와 비교하여 함수 호출 시 매개변수가 생략되었는지 확인

   ```javascript
  function showMessage(text) {
  	if (text === undefined) {
  		text = '빈 문자열';
  	}
  	alert(text);
  }
  
  showMessage();		// 빈 문자열
  ```

  * `||` 사용 : 매개변수가 생력되었거나 빈 문자열("")이 넘어오면 변수에 '빈 문자열'이 할당

  ```javascript
  function showMessage(text) {
  	text = text || '빈 문자열';
  	...
  }
  ```

  * `??` 사용 : 매개변수가 넘어오지 않으면 'unknown'을 출력

  ```javascript
  function showCount(count) {
	alert(count ?? "unknown");
  }

  showCount(0);	// 0
  showCount();	// unknown
  ```
 

### 반환 값(return value)

* 함수를 호출했을 때 함수를 호출한 곳에 반환되는 값
* 지시자 `return` 사용
* 지시자 `return`을 만나면 함수 실행이 즉시 중단되고 함수를 호출한 곳에 값을 반환

```javascript
function sun(a, b) {
	return a + b;
}

let result = sun(1, 2);

alert(result);	// 3
```

* 함수 하나에 여러 개의 `return`문 가능 (if문 사용)
* 지시자 `return`만 명시하는 것도 가능 (함수가 즉시 종료됨)
* `return`문이 없거나 `return` 지시자만 있는 함수는 `undefined`를 반환
* `return`과 값 사이에 줄 삽입 금지 (자바스크립트는 return문 끝에 자동으로 세미콜론을 넣기 때문)

```javascript
return
	(some + long + expression + or + f(a) + f(b))
```

표현식을 여러 줄에 걸쳐 작성하는 방법 (표현식이 `return`지시자가 있는 줄에서 시작하도록 작성)

```javascript
return (
	some + long + expression
	+ or + f(a) + f(b)
)
```

 

### 함수 이름짓기

함수가 어떤 동작을 하는지 축약해서 설명해주는 동사를 접두어로 붙여 함수 이름을 만드는 게 관습 (팀 내에서 그 뜻이 합의된 접두어만 사용)
* `"show"` - 무언가를 보여줌
* `"get"` - 값을 반환함
* `"clac"` - 무언가를 계산함
* `"create"` - 무언가를 생성함
* `"check"` - 무언가를 확인하고 불린값을 반환함


### 함수는 간결하고, 한 가지 기능만 수행할 수 있도록 만들어야 한다.

* 함수가 길어질 경우에 함수를 분리하여 작성할 것을 권유한다.
* 간결하게 만들면 테스트와 디버깅이 쉬워지고, 함수 그 자체로 주석의 역할을 한다.
* 자기설명적(self-describing) 코드 : 이름만 보고도 어떤 동작을 하는지 알 수 있는 코드 -> 코드가 정돈되고 가독성이 높아진다.


참고 : https://ko.javascript.info/