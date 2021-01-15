# Compnent Sacn

스코프가 싱글톤이라 초기에 구동 시간이 오래걸린다는 단점이 있다. <!-- 7:08 --> 때문에 구동 시간에 예민하다면 funcional을 이용해도된다.

funcional은 리플렉션, 프록시 등 성능에 악영향을 미치는 요소를 사용하지 않는다.

<!-- ~13:10 -->
> 참고
> 
> 컴포넌트 스캔은 직접 등록(`@Bean`을 이용하거나 funtional을 이용한 방법)하기 전에 일어난다.
> ApplicationContext 만들 때 생성되기 때문에 구동이 느려질 수 있다.

Component Scan의 역할
가장 중요한 속성 두개
스테레오 타입
평셔널한 빈 등록 방법

백선생 曰: 성능때문에 컴포넌트 스캔 대신 펑셔널을 사용하는 건 좀... `@Bean`을 대체할만한 방법인 것 같긴하다.

---

## 범위
크게 두가지가 존재한다.
- 싱글톤
- 프로토 타입

## 문제
싱글톤 빈 스코프 클래스 안에 프로토 타입 빈 스코프 클래스가 있다면, 전자의 객체를 계속 주입 받을 때 안에 있는 객체도 다 같은 현상이 일어난다 (원래 의도는 다 다른 객체여야함).

이걸 해결하는 방법이 두가지

<!-- 14:40 -->
## 해결 1. proxyMod 옵션 사용
프로토 타입 빈 스코프에 해당하는 클래스를 프록시로 감싸는 방법

싱글톤 타입 빈 스코프 클래스가 프로토 타입 빈 스코프 클래스를 직접 참조하면 안되기 때문에 매번 생성해 줄 수있는 프록시로 감쌈.

CG 라이브러리: 클래스도 프록시를 만들 수 있게 해주는 서드파티 라이브러리 (원래 자바 JDK안에 있는 다이나믹 프록시는 인터페이스 프록시밖에 못만듬)

실질적으론 프로토 타입 빈 스코프 클래스를 주입해줌(상속받기 때문에 사실상 타입이 같음)

"프록시 패턴"이라는 용어를 알아두자

성능에 영향이 있고 다소 복잡하다.

### 해결 2. `ObjectProvider<Object>`

``` java
@Component
public class Single {

    @Autowired
    private ObjectProvider<Proto> proto;

    publuc Proto getProto() {
        return proto.getIfAvailable();
    
    }
}
```

백선생 曰: 코드 자체에 스프링 코드가 들어가기 때문에 개인적으론 선호하치 않음.



# ApplicationContext
`ApplicationContext`은 많은 클래스를 상속받고 있는데 `EnvironmentCapable`이라는 애가 있다.
## Environment가 제공하는 기능

### profile
- profile: 빈들의 묶음, 어떤 환경
- 각각의 환경에 다른 빈들을 써야할 경우, 특정 환경에만 사용해야하는 빈이 있는 경우 등...

프로파일 주는 방법
- IDE 옵션1: 액티브 프로파일 직접 설정 // 우리가 할 수 없을수도 버전
- IDE 옵션2: VM 명령어 옵션`-Dspring.profiles.active=[프로파일 이름]`
- 어노테이션 옵션: `@ActiveProfile` -> 코드 고정이기 때문에 테스트 상황에서만
- 

클래스나 메소드 단에서 `@Component`나 `@Bean` 어노테이션과 함께 사용 가능

조건 설정 넣을 수 가능
- and `&`
- or `|`
- not `!`

ex) 
`@Profile("!prod")`

### property
- application에 등록된 계층형 key-value로 이루어진 설정값
- 다양한 방법으로 접근하여 활용할 수 있음
- 보통 resource 아래에 `*.property` 파일을 만들고 그곳에 설정값을 입력

### property 사용
아래에 언급한 방법 외에도 여러가지 다른 방법이 있다.
- `@PropertySource`
    - 설정값을 사용할 클래스에서 `@PropertySource("[경로]")` 어노테이션 적용
    - `environment.getProperty("[이름]");`으로 꺼내서 사용
    - 여기서 어떤 경로의 프로퍼티 파일을 사용할지에 대한 우선순위 존재
        - 어노테이션 설정보다 VM 명령어 옵션 설정이 우선
- `@Value`
    - 프로퍼티를 적용할 필드에 `@Value("&{[이름]}")` 어노테이션 적용