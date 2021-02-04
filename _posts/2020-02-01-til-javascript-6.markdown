---
layout: post
title: "[TIL/Javascript] 자바스크립트의 자료형"
date: 2020-02-01 23:52:23 +0900
category: Javascript
comments: true
---

## 1. 자료형

* 동적 타입(dynamically typed) 언어 : 자료의 타입은 있지만 변수에 저장되는 값의 타입은 언제든지 바꿀 수 있는 언어


### 숫자형 (number type)

* 정수 및 부동소수점 숫자(floating point number)를 나타낼 때 사용
  * 정수의 한계는 ±2^53^
* 연산 : `+`, `-`, `*`, `/`
* 특수 숫자 값(special numeric value) 포함
  * Infinity : 무한대, 어떤 숫자든 0으로 나누면 얻을 수 있다.
  * NaN : 계산 중에 에러가 발생했다는 것을 나타내주는 값 (부정확하거나 정의되지 않은 수학 연산을 하더라도 에러가 나타나지 않음)


### BigInt

* 길이에 상관없이 정수를 나타낼 수 있다.
* 정수 리터럴 끝에 `n`을 붙이면 만들 수 있다.
* Firefox, Chrome, Edge에서만 지원한다. 

```javascript
const bigInt = 1234567890123456789012345678901234567890n;
```


### 문자형

* 빈 문자열이나 글자들로 이루어진 문자열을 나타낼 때 사용한다.
* 따옴표로 묶어서 표현한다.
  1. 큰따옴표 : `"Hello"`
  2. 작은따옴표 : `'Hello'`
  3. 역따옴표 : ``Hello``
* 큰따옴표와 작은따옴표는 차이가 없다.
* 변수나 표현식을 `${...}` 안에 넣고 역 따옴표로 감싸주면, 변수나 표현식을 문자열 중간에 넣을 수 있다.

```javascript
let name = "soyeon";
alert(`Hello, ${name}!`);// Hello, soyeon!
alert(`${3 + 4}`);// 7
```


### 불린형

* `true`와 `false` 두 가지 값밖에 없는 자료형
* 비교 결과를 저장할 때 사용

```javascript
let isGreater = 4 > 1;
alert(isGreater);// true
```


### `null` 값

* '존재하지 않는 값', '비어 있는 값', '알수 없는 값'을 나타낼 때 사용
* 어느 자료형에도 속하지 않는 값 (독립 자료형)


### `undefined` 값

* '값이 할당되지 않은 상태'를 나타낼 때 사용
  * 변수는 선언했지만 값을 할당하지 않은 경우 해당 변수에 자동으로 할당
  * 직접 할당하는 것도 가능하지만, 권장하지 않음
* 자신만의 자료형 형성 (독립 자료형)


### 객체와 심볼

* 객체(object) : 복잡한 데이터 구조를 표현할 때 사용한다.
  * 객체형을 제외한 다른 자료형은 한 가지만 표현할 수 있기 때문에 원시 자료형
* 심볼(symbol) : 객체의 고유한 식별자를 만들 때 사용한다.


### typeof 연산자

* 피연산자의 자료형을 문자열로 반환한다.
* 두 가지 문법을 지원한다. (동일한 결과)
  1. 연산자 : `typeof x`
  2. 함수 : typeof(x)

```javascript
typeof undefined// "undefined"
typeof 0// "number"
typeof null// "object"
typeof alert// "function"
```
* `null` : 하위 호환성을 유지하기 위해 오류를 수정하지 않고 남겨둔 상황 (언어 자체의 오류)
* `alert` : 함수이므로 "function" 반환
 
