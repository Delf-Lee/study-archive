# IoC(Inversion of Control)과 DI(Dependency Injection)

> **IoC(Inversion of Control)**
> 의존관계 주입(Dependency Injection)이라고도 하며, 어떤 객체가 사용하는 의존 객체를 직접 만들어 사용하는게 아니라, **주입 받아 사용**하는 방법을 말함.

라고 백선생님은 이야기하셨는데... 두 개념은 강한 관련이 있지만 완벽히 대체할 수 있는 같은 의미는 아니라고 생각한다.

## DI(Dependency Injection)
직역하면 **의존성 주입**

### 의존성
"의존성 있다"란 두 객체(클래스) 사이에 연관관계가 있어 메시지를 보낼 수 있는 상태를 뜻한다.

메시지를 보내기 위해서, 즉 메서드를 호출하기 위해서는 그 객체의 레퍼런스를 **알고 있어야한다**. 이 레퍼런스는 호출하는 메서드 파라미터의 형태로 받을수도 있고, 아예 필드 형태로 가지고 있을 수 있다.

이 레퍼런스를 전달하는 것 자체가 '의존성 주입'이다.

Spring에서는 대개 그 의미를 조금 좁혀서, *"필드로 어떤 객체의 레퍼런스를 갖고 있고 이를 외부로부터 주입받는 것"* 을 의존성 주입이라고 말한다.

#### 왜?
한마디로 요약하자면, **결합도를 낮추고 재사용성을 늘리기 위해서**이다.

<!-- 어떤 IT 회사에서 일할 사람이 필요한데, 그게 꼭 특정 사람(예를들어 나)일 필요는 없다. 개발자의 역량을 갖추고 있다면 누구든 들어갈 수 있다. -->

어떤 객체를 생성할 때, 필드 초기화를 내부 자체적으로 한다면 변경의 여지가 없어진다. 이는 이 클래스를 재사용하는데 있어 치명적이다.

## IoC(Inversion of Control)
직역하면 **제어의 역전**

엄밀히 말하면 스프링에서만 쓰이는 개념은 아니다.

> 제어의 역전 이란 어떠한 일을 하도록 만들어진 프레임워크에 제어의 권한을 넘김으로써 클라이언트 코드가 신경 써야 할 것을 줄이는 전략이다.
> 이것을 제어가 역전 되었다 라고 하며, 일반적으로 라이브러리는 프로그래머가 작성하는 클라이언트 코드가 라이브러리의 메소드를 호출해서 사용하는 것을 의미 한다.
>  프레임워크를 규정하는 특성은 프레임워크의 메소드가 사용자의 코드를 호출 한다는데 있다.
> 
> 출처: https://vandbt.tistory.com/43 [소프트웨어 디자인- Design Software by vandbt]

상당히 고전적인 설명이지만 가장 근본적이기도하다. 여기서는 다음과 같은 언급을 하기도한다.

> 마틴 파울러는 그의 글 Inversion of Control Containers and the Dependency Injection pattern 에서 IoC 라는 용어가 너무 일반적이며 모호하므로 앞으로는 Dependency Injection 이라는 용어를 사용하겠다 라고 말하고 있다.

백선생님이 IoC를 DI로 퉁치는 이유가 이것인 것 같다.

내 생각은 **"이런 프레임워크가 제공해주는 제어의 역전을 이용하기 위해서는 의존성 주입이 가능하도록 설계해야한다."** 이다.

아예 같은 개념이라고 보기에는 애매하지만 확실히 밀접한 관련이 있긴한 것 같다.

이걸 더 이해하기 위해서는 IoC 컨테이너에 대해서 알 필요가 있을 것 같다.


## IoC 컨테이너
### 컨테이너
컨테이너라는 개념 자체는 내가 작성한 코드나 설정등을 기반으로 각종 처리를 위임받은 독립적인 존재다. IoC 컨테이너 말고도 톰캣이나 도커에서도 곧잘 보이는 용어이다.

### 역할
스프링 프레임워크도 객체에 대한 생성 및 생명주기를 관리할 수 있는 기능을 제공한다.

- 객체를 생성하고 의존성을 관리한다.
- 생성한 객체의 라이프사이클에 대한 권한을 가진다.

#### 중요 인터페이스
`BeanFactory`상속받은 `ApplicationContext`객체를 이용해서 접근할 수 있다.
``` java
public interface ApplicationContext extends EnvironmentCapable, ListableBeanFactory, HierarchicalBeanFactory, MessageSource, ApplicationEventPublisher, ResourcePatternResolver {

    @Nullable
    String getId();

    String getApplicationName();

    String getDisplayName();

    long getStartupDate();
 
    @Nullable
    ApplicationContext getParent();

    AutowireCapableBeanFactory getAutowireCapableBeanFactory() throws IllegalStateException;
}
```

## Reference
- [제어의 역전(Inversion of Control, IoC) 이란? // develogs](https://develogs.tistory.com/19)
- [스프링이 도대체 뭐란 말인가? // 거짓말](http://springmvc.egloos.com/487497)
- [IoC, DI란 무엇일까 // 백문이불여일타](https://biggwang.github.io/2019/08/31/Spring/IoC,%20DI%EB%9E%80%20%EB%AC%B4%EC%97%87%EC%9D%BC%EA%B9%8C/)
- [토비의 스프링 - IoC 컨테이너와 DI // Gunju Ko](https://gunju-ko.github.io/toby-spring/2019/03/25/IoC-%EC%BB%A8%ED%85%8C%EC%9D%B4%EB%84%88%EC%99%80-DI.html)