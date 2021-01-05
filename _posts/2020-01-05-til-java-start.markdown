---
layout: post
title: "[TIL/JAVA] 자바의 특징과 프로그램 작성"
date: 2020-01-05 23:52:23 +0900
category: Java
comments: true
---

## 1. 자바의 특징

* 운영체제에 독립적이다.
  * 자바 응용프로그램은 자바가상머신(JVM)과 통신하고 JVM이 응용프로그램으로부터 전달받은 명령을 해당 운영체제가 이해할 수 있도록 변환하여 전달한다.
* 상속, 캡슐화, 다형성이 잘 적용된 객체지향언어이다.
* 가비지컬렉터가 자동 메모리 관리를 해준다.
* 시스템과 관계없이 멀티쓰레드를 지원한다.
* 동적 로딩(Dynamic Loading)을 지원하여 필요한 시점에 클래스를 로딩하여 사용할 수 있다.


## 2. 프로그램 작성 규칙

```java
class 클래스이름 {
  public static void main(String[] args){ // main 메서드의 선언부

  }
}
```

* public class가 하나 이하 여야한다.
* 소스파일의 이름
  * public class가 있는 경우 public class의 이름으로 지정한다.
  * public class가 없는 경우 class의 이름 중 하나로 지정한다.
* 하나의 자바 애플리케이션에는 main메서드를 포함한 클래스가 반드시 하나는 있어야 한다.
  * main메서드의 호출로 시작하여 첫문장부터 마지막 문장까지 수행하고 종료된다.

### 컴파일 및 실행 과정

1. 소스 파일(Hello.java) 작성 후 컴파일
2. 클래스 파일(Hello.class) 생성 후 실행
3. 실행 결과 출력

cmd에서 java 파일이 저장된 경로에서 컴파일 및 실행 <br>
(Hello.java를 컴파일하고 실행할 경우)

---
    cd C:\Users         // 경로 이동 명령어 cd
    javac Hello.java    // 컴파일 명령어 javac
    java Hello          // 실행 명령어 java

---

## 3. 주석
* 범위 주석 /* */
* 한 줄 주석 //