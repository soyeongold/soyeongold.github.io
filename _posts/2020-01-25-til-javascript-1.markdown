---
layout: post
title: "[TIL/Javascript] 자바스크립트 개요, 형변환, 반복문, 주석"
date: 2020-01-25 23:52:23 +0900
category: Javascript
comments: true
---

## 1. 웹 페이지에 자바스크립트 삽입

* `<script>` 태그 안에 위치

```
<html>
<body>
<script>
    // 자바스크립트 삽입
</script>
</body>
</html>
```

* 외부 스크립트 src 속성 사용

```
<script src="path/to/script.js"></script>
```

## 2. 형 변환
* 문자형으로 변환 : String(value)
* 숫자형으로 변환 : Number(value)

|전달받은 값|형 변환 후|
|:---:|:---:|
|undefined|NaN|
|null|0|
|true and false|1과 0|
|string|문자열의 처음과 끝 공백 제거, 공백 제거 후 문자열이 없다면 0, 변환 실패 시 NaN|

* 불린형으로 변환 : Boolean(value)

|전달받은 값|형 변환 후|
|:---:|:---:|
|0, 빈 문자열, null, undefined, NaN|false|
|그 외의 값|true|

## 3. 반복문
### while 반복문

```javascript
while(condition) {
	// 코드 (body)
}

```
* condition(조건)이 truthy이면 코드 실행, 조건이 truthy인 동안에 본문 계속 실행

### do...while 반복문
```javascript
do {
	// 반복문 본문
} while (condition);
```
* 본문이 먼저 실행되고, 조건을 확인한 후 조건이 truthy인 동안에 본문 계속 실행

### for 반복문
```javascript
for (begin; condition; step) {
	// 반복문 본문
}
```
* begin 실행
-> condition이 truthy일 경우 -> body 실행 -> step 실행
-> .. 반복
* 인라인 변수 선언 : 반복문 안에서 변수 선언 (반복문 안에서만 접근 가능)
* 구성 요소(begin, condition, step) 생략 가능

### 반복문 빠져나오기 : break
* 무한 반복문 + break : 본문 가운데 혹은 본문 여러 곳에서 조건을 확인해야 하는 경우

### 다음 반복으로 넘어가기 : continue
* 현재 반복을 종료시키고 다음 반복으로 강제로 넘어감 (조건을 통과할 때 사용)

### break/continue와 레이블
* 중첩 반복문을 빠져나와 바깥의 반복문으로 갈 수 있게 해주는 유일한 방법

```javascript
outer:
for (let i = 0; i < 3; i++) { 
	for ( let j = 0; j < 3; j++) {
		let input = prompt('(${i}, ${j})의 값', '');
		if (!input) break outer;
	}
}
```

## 4. 주석
* 한 줄 주석  //
* 여러 줄 주석  /* */
  * 중첩 주석 지원 안함