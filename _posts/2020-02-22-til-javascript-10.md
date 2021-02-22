```
---
layout: post
title: "[TIL/Javascript] 자바스크립트의 Promise"
date: 2020-02-04 23:52:23 +0900
category: Javascript
comments: true
---
```



## Promise

프라미스(Promise)는 '제작 코드'와 '소비 코드'를 연결해주는 특별한 자바스크립트 객체이다.

* 제작 코드(producing code) : 원격에서 스크립트를 불러오는 것 같은 시간이 걸리는 일
* 소비 코드(consuming code) : '제작 코드'의 결과를 기다렸다가 이를 사용, 이 때 소비 주체(함수)는 여럿이 될 수 있다.



```javascript
let promise = new Promise(function(resolve, reject) {
	// executor (제작 코드)
});
```

* executor는 `new Promise`가 만들어질 때 자동으로 실행된다.

* `resolve`와 `reject`는 자바스크립트가 제공하는 콜백이다. executor에서 결과를 얻으면 콜백 중 하나를 반드시 호출해야 한다.
  * `resolve(value)` : 일이 성공적으로 끝난 경우, 그 결과를 나타내는 `value`와 함께 호출
  * `reject(error)` : 에러 발생 시 에러 객체를 나타내는 `error`와 함께 호출

* `promise` 객체의 내부 프로퍼티

  * `state` : 처음엔 `pending`이었다가, 

    resolve가 호출되면 `fulffiled`, reject가 호출되면 `rejected`로 변한다.

  * `result` : 처음엔 `undefined`이었다가, 

    resolve가 호출되면 `value`, reject가 호출되면 `error`로 변한다.

* 첫 번째 `reject/resolve` 호출만 고려 대상이기 때문에 두 번째 `resolve/reject` 부터는 무시된다.



![](C:\Users\kimsoyeon\Desktop\캡처.PNG)



### 소비함수 : then, catch, finally

#### then

```javascript
promise.then(
	function(result) { /* 결과(result)를 다룬다. */ },
    function(result) { /* 에러(error)를 다룬다. */ }
);
```

* 첫 번째 인수 : 프라미스가 이행(fulfilled)되었을 때 실행되는 함수이고, 여기서 실행 결과를 받는다.

* 두 번째 인수 : 프라미스가 거부(rejected)되었을 때 실행되는 함수이고, 여기서 에러를 받는다.

  (성공적으로 처리된 경우만 다르고 싶다면 인수를 하나만 전달)



예시)

```javascript
let promise = new Promise(function(resolve, reject) {
    setTimeout(() => resolve("done!"), 1000);
});

// resolve 함수는 .then의 첫 번째 함수(인수)를 실행
promise.then(
	result => alert(result),	// 1초 후 "done!"을 출력
    error => alert(error)
);
```



#### catch

```javascript
promise.catch(function() { /* 에러를 다룬다. */ });
```

* 에러가 발생한 경우만 다루고 싶을 때 사용한다.

* `.then(null, f)`과 동일하게 작동한다.



#### finally

```javascript
promise.finally(function() { /* 프라미스가 처리되면 항상 실행 */ });
```

* 프라미스가 처리되면(이행, 거부)되면 실행된다.
* `then(f, f)`와 유사하게 작동한다.
* `finally` 핸들러의 `then(f, f)`과 차이점
  * 인수가 없다. (이행/거부되었는지 알 수 없음)
  * 자동으로 다음 핸들러에 결과와 에러를 전달한다.



예시)

```javascript
new Promise((resolve, reject) => {
    throw new Error("에러 발생!");
})
	.finally(() => alert("프라미스가 준비되었습니다."))
	.catch(err => alert(err));				// catch에서 에러 객체를 다룰 수 있다.
```



참고 : [](https://ko.javascript.info/promise-basics)

