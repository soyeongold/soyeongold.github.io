---
layout: post
title: "[TIL/Javascript] 바닐라 JS로 크롬 앱 만들기 정리"
date: 2020-02-08 23:52:23 +0900
category: Javascript
comments: true
---

NomadCoders의 '바닐라 JS로 크롬 앱 만들기' 정리한 내용이다.



[clock.js]

### Javascript 시작함수 사용

```
function init() {
	// ...
}

init();
```



###  DOM 함수 사용

```
document.querySelector(element)
```

* html에 있는 class를 javascript 상수 객체로 가져온다.
* document 객체의 자식을 탐색하여 element에 해당하는 자식을 반환

 

###  '?' 삼항 연산자를 이용

```
clockTitle.innerText = `${hours < 10 ? `0${hours}` : hours} : 
						${minutes < 10 ? `0${minutes}` : minutes} :
						${seconds < 10 ? `0${seconds}` : seconds};
```

* 시계 숫자를 두 자리로 표현

 



[greetting.js, todo.js]

### Local Storage

정보를 유저 컴퓨터에 저장하는 방법

* 확인 : 개발자도구 - application - local storage



#### 기본 API

```
// 키에 데이터 쓰기
localStorage.setItem("key", value);

// 키로부터 데이터 읽기 (해당 데이터 반환)
localStorage.getItem("key");
```

- API를 사용하여 이름과 Todo들을 저장한다.



#### 주의사항

- localStorage에는 자바스크립트의 data를 저장할 수 없다. (오직 string만 가능)
- JSON 형태로 데이터를 읽고 쓰기

```javascript
// Javascript 객체를 string으로 변환  (LocalStorage에 데이터를 쓸 때 사용)
JSON.stringify();

// string을 Javascript 객체로 변환 (LocalStorage에서 데이터를 읽어올 때 사용)
JSON.parse();
```

 

### classList

`element.className`을 통해 엘리먼트의 클래스 목록에 접근하는 방식을 대체하는 방법이다.

#### 메서드

* `add(String [, String ...])` : 지정한 클래스 값을 추가
* `remove(String [, String ...])` : 지정한 클래스 값을 제거
* `contains(String)` : 지정한 클래스 값이 엘리먼트의 class 속성에 존재하는지 확인
* `replace(oldClass, newClass)` : 존재하는 클래스를 새로운 클래스로 교체
* `toggle(String [, force])` : 클래스값이 있는지 체크하고 없으면 추가하고 있으면 제거

```
const title = document.getElementById("title");
const CLICKED_CLASS = "clicked";

function handleClick(){
    const hasClass = title.classList.contains(CLICKED_CLASS);
    if(hasClass){
        title.classList.remove(CLICKED_CLASS);
    }else{
        title.classList.add(CLICKED_CLASS);
    };
};

```



### <form> : 값을 입력받아서 event를 발생시키는 태그

* 기본 동작 : 값을 다른 곳으로 보내고 새로고침을 한다.

* 기본 동작 막기 : `event.preventDefault()` 호출

* 입력받은 값 가져오기  (`value` 프로퍼티 사용)

  ```
  const input = form.querySelector("input");
  // ...
  const inputValue = input.value;
  ```

  



[bg.js]

### `ParentNode` 객체 추가 메소드

* `append() `: ParentNode의 맨 뒤에 자식 요소로 삽입된다.
  * 반환하는 값이 없다. `appendChild()`는 추가한 Node 객체를 반환한다.

* `prepend()` : ParentNode의 맨 앞에 자식 요소로 삽입된다.
  * `undefined` 반환

```
const body = document.querySelector("body");
const p = document.createElement("p");
const span = document.createElement("span");

body.append(p);
body.prepend(span);

console.log(body.childNodes);		// NodeList [<span>, <p>]
```





[weather.js]

### navigator API

#### API 호출하기

- weather API를 API키와 `fetch()` 를 사용하여 호출한다.
- Javascript는 필요할 때 서버에 네트워크 요청을 보내고 새로운 정보를 받아오는 일을 할 수 있다. 새로 고침이 없이도 가능하다.

##### fetch()

```
let response = fetch(url[, options]);
```

* `url` : 접근하고자 하는 URL
* `options` : method나 header 등을 지정할 수 있다. 아무것도 넘기지 않으면 `GET` 메서드로 진행되어 url로부터 콘텐츠가 다운로드된다.
* fetch() 호출 시 : 네트워크 요청을 보내고 Promise가 반환된다.

* 응답 과정
  1. 반환받은 Promise가 내장 클래스 Response의 인스턴스와 함께 이행(fulfilled) 상태가 된다.
  2. 추가 메서드를 호출하여 응답 본문을 받는다.

* 응답 프로퍼티
  * `status` : HTTP 상태코드
  * `ok` : 불린 값, status가 200~299일 경우 true

* Promise를 기반으로 하는 메서드 (추가 메서드)
  * `response.text()` : 응답을 읽고 텍스트를 반환
  * `response.json()` : 응답을 JSON 형태로 파싱
  * `response.formData()` : 응답을 FormData 객체 형태로 반환

```
fetch(
        `https://api.openweathermap.org/data/2.5/weather?lat=${lat}&lon=${lng}&appid=${API_KEY}&units=metric`
        )
    .then(function(response) {
        return response.json();
    })
    .then(function(json) {
		const temperature = json.main.temp;
        const place = json.name;
        weather.innerText = `${temperature}° \n ${place}`;
	});
```

* fetch()를 완료하여 나온 데이터를 then(함수)로 함수를 호출하여 JSON형태로 파싱하고, JSON 데이터가 준비되면 출력한다.



#### 사용자의 현재 위치 가져오기

```
navigator.geolocation.getCurrentPosition(success[, error[, options]]);
```

* `success` : 위치를 가져오는데 성공했을 때 실행하는 함수 (콜백함수)
* `error`: 위치를 가져오는데 실패했을 때 실행하는 함수 (콜백함수)
* `options` : `PositionOptions` 객체 (Option 설정 객체)