# 패키지
### index
- package 키워드
- import 키워드
- 클래스패스
- CLASSPATH 환경변수
- -classpath 옵션
- 접근지시자

## `package` 키워드
### 패키지란?
> 하나의 의미를 갖는, 물리적으로 분리된 자바 파일의 모음 혹은 그런 모음의 단위
- 쉽게 표현하자면 "자바 파일을 담은 폴더"
- 여기서 자바 파일이라 함은 class, interface, enum 등을 의미(이하 셋을 클래스로 통일히여 표현)

### FQCN(Fully Qualified Class Name)
모든 클래스는 정의된 이름이 있고 패키지에 포함되어 있다. 이러한 위치와 클래스명을 모두 명시한 이름을 FQCN이라고 하며, 이것으로 하나의 클래스를 특정할 수 있다.

패키지와 클래스 사이는 `.`으로 구분한다. 예를들어 자바의 `String` 클래스는 다음과 같이 표현할 수 있다.
``` java
java.lang.String
```

### `package` 키워드
클래스가 포함될 패키지를 지정할 때 사용된다. 클래스 파일 최상단에 `package` + `클래스의 FQCN`로 명시하면 된다.

```
dev
└── delf
    └── livestudy
        └── week7
            └── HelloWorld.java
```
이를테면 다음과 같은 패키지 구조에서는 아래와 같이 표현할 수 있다.

``` java
package dev.delf.livestudy.week7;

class HelloWorld { 
    // ...
}
```
### 명명 규칙/관례
- package의 이름은 **모두 소문자**이어야 하며, **자바의 키워드(예약어)** 는 사용할 수 없다.
- 충돌 방지를 위해 보통 도메인의 역순으로 명명한다.
  - ex) `com.chat.application.domain`


## import 키워드
다른 패키지의 클래스를 참조할 때 클래스를 참조할 때 사용한다. 이 역시 `import` + `클래스의 FQCN`로 명시하면 된다.

동일 패키지 내에 있는 클래스는 `import` 없이 참조할 수 있다.
``` java
import com.chat.application.domain.Room; // 다른 패키지의 클래스
import com.chat.application.domain.User;

public class TalkService {
    Room room = new Room();
    User user = new User();
}
```
동패키지 내의 모든 클래스를 참조하고 싶다면 와일드 카드로 표시할 수 있다.

``` java
import com.chat.application.domain.*; // 와일드 카드

public class TalkService {
    Room room = new Room();
    User user = new User();
}
```

## 클래스 패스
말 그대로 클래스를 찾기위한 경로.

- 소스 코드(`*.java`파일)를 컴파일하면 JVM이 실행가능한 바이트 코드(`*.class`파일)가 생행된다
- jre가 이 `*.class`파일이 포함된 명령을 실행하려면, 먼저 이 파일을 찾을 수 있어야 한다
  - 이때 지정된 경로를 사용하는데, 이 경로가 바로 **클래스 패스**
- jre는 클래스 패스에 지정된 경로를 모두 검색해서 특정 클래스에 대한 코드가 포함된 .class 파일을 찾는다
- 클래스 패스를 지정할 수 있는 방법은 두 가지가 있다
  - 환경 변수 CLASSPATH를 사용하는 방법
  - java runtime에 -classpath 플래그를 사용하는 방법

## CLASSPATH 환경변수

jvm이 클래스 패스를 찾는 것 뿐만 아니라, 다른 많은 프로세스에서도 비슷한 맥락으로 적절한 경로에서 파일들을 참조한다. 이런 경로들을 운영체제단에서 한번에 관리하는데, 이를 **환경변수**라고 한다.

jvm가 찾아갈 클래스 패스 경로의 기본값도 여기에서 지정할 수 있다. 그 방법은 여러가지. GUI 설정으로도, 명령어 설정으로도 변경할 수 있다.


## -classpath 옵션

환경변수에서 지정해준 클래스 패스 이외에 바이트 코드를 실행할 때, 직접 클래스 패스를 따로 지정해줄 수 있다. 이때 사용하는 옵션이 -classpath 옵션.

``` unix
javac -classpath [경로1];[경로2] [실행 파일]
```
경로가 둘 이상이면 세미콜론`;`으로 여러개를 지정해 줄 수 있다.

## 접근지시자
어떤 변수나 클래스가 접근할 수 있는 범위를 지정해주는 키워드

객체지향에서 캡슐화를 통한 적절한 정보 은닉, 그리고 나아가 추상화를 도와주는 개념이다.

`private`, `protect`, `public`이외에도, 패키지를 기준으로 접근을 제어하는 키워드도 존재한다. `default`


### Reference
- [개발배말 - [Live Study] 7주차 과제: 패키지](https://blog.baesangwoo.dev/posts/java-livestudy-7week/)
- [코딩하는 오징어 - 자바 클래스패스(classpath)란?](https://effectivesquid.tistory.com/entry/%EC%9E%90%EB%B0%94-%ED%81%B4%EB%9E%98%EC%8A%A4%ED%8C%A8%EC%8A%A4classpath%EB%9E%80#recentEntries)