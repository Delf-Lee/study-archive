# 2장 객체의 생성과 삭제
- 객체를 만들어야 하는 시점과 그 방법
- 객체 생성을 피해야 하는 경우와 그 방법
- 적절한 순간에 객체가 삭제되도록 보장하는 방법
- 객체 삭제 전에 반드시 이루어져야 하는 청소 작업

## 규칙 1 - 생성자 대신 정적 팩터리 메서드를 사용할 수 없는지 생각해 보라
- 생성자를 사용하는 것 이외에 **정적 팩터리 메서드**를 이용해 객체를 생성 할 수 있다.
- 지다인 패턴의 **팩터리 메서드 패턴**과는 다르다.  

### 장점1. 생성자와는 달리 정적 팩터리 메서드에는 이름(name)이 있다.
- 사용하기 쉽고, 가독성도 좋아진다.
- 같은 시그니처를 갖는 생성자를 여러 개 정의할 필요가 있을 때는 그 생성자들을 정적 팩터리 메서드로 바꾸고, 메서드 이름을 보면 차이가 명확히 드러나도록 작명에 신경쓰자
### 장점2.  생성와는 달리 호출할 때마다 새로은 객체를 생성할 필요가 없다.
- 만들어 둔 객체를 활용할 수도 있고 객체를 캐시 해놓고 재사용하고 불필요하게 거듭 생성되는 일을 피할 수 있다.
- 이 기법은 경량(Flyweight) 패턴과 유사하다. 


#### 개체 통제 클래스(instance-contrilled class)  
정적 팩터리 메서드를 사용하면 같은 객체를 반복해서 반환할 수 있으므로 어떤 시점에 어떤 객체가 얼마나 존재할지를 정밀하게 제어할 수 있다. 그런 기능을 갖춘 클래스를 **개체통제 클래스**라고 부른다.

- '개채 통제 클래스'의 사용 이유
    - 개체 수를 제어하면 싱글턴(singleton)패턴을 따르도록 할 수 있다. (규칙3)
    - 객체 생성이 불가능한 클래스를 만들 수 있다. (규칙4)
    - 변경이 불가능한 클래스의 경우(규칙15) 두 개의 같은 객체가 존재하지 못하도록 할 수도 있다. 
        - 연산자 비교(==)가 가능해져 성능이 향상될 수 있다.
        - 열거형(enum) 자료형(규칙30)이 이 기법을 사용한다.

### 장점3. 생성자와는 달리 반환값 자료형의 하위 자료형 객체를 반환할 수 있다.
- 반환되는 객체의 클래스를 훨씬 유연하게 결정할 수 있다.
- 인터페이스 기반 프레임워크(interface-based framework)구현에 적합하다.(규칙18)
- 심지어 <u>정적 팩터리 메서드가 반환하는 객체의 클래스</u>는 정적 팩터리 메서드가 정의된 <u>클래스의 코드가 작성되는 순간에 존재하지 않아도</u> 무방하다.
- JDBC 와 같은 *서비스 제공자 프레임워크*의 근간을 이루는 것이 바로 이런 유연란 정작팩터리 메스드들이다.

서비스 제공자 프레임워크의 세가지 핵심 컴포넌트 (+하나 더)
1. **서비스 인터페이스**: 서비스 제공자가 구현한다.
2. **제공자 등록 API**: 구현체를 시스템이 등록하여 클라리언트가 쓸 수 있도록 한다.
3. **서비스 접근 API**: 클라이언트에게 실제 서비스 구현체를 제공한다.
4. 서비스 제공자 인터페이스: 서비스 제공자가 구현한다.

서비스 제공자 인터페이스의 대략적인 모습
``` java

// 서비스 인터페이스
public interface Service {
}

// 서비스 제공자 인터페이스
public interface Provider {
    Service newService();
}

// 서비스 등록과 접근에 사용되는 객체 생성 불가능 클래스
public class Services {
    private Service() {} // 객체 생성 방지 (규칙4)

    // 서비스 이름과 서바스 간 대응관계 보관
    private statis final Map<String, Provider> providers = new ConcurrentHashMap<String, Provider>();
    public static final String DEFAULT_PROVIDER_NAME = "<def>";

    // 제공자 등록 API
    public static void registerDefaultProvider(Provider p) {
        registerProvider(DEFAULT_PROVIDER_NAME, p);
    }

    public static void registerProvider(String name, Provider p) {
        providers.put(name, p);
    }
    // 서비스 접근 API
    public static Service newInterface() {
        return newInterface(DEFAULT_PROVIDER_NAME);
    }

    public static Service newInstance(String name) {
        Provider p = provider.get(name);
        if(p == null) {
            throw new IllegalArgumentException("No provider registered with name: " + name);
        }
        return p.newSerivce();
    }
}
```

### 장점4. 형인자 자료형(parameterized type) 객체를 만들때 편리하다.
``` java
Map<String, List<String>> = m = new HashMap<String, List<String>>();
```
자료형 명세를 중복하면 형인자가 늘어남에 따라 길고 복잡한 코드가 만들어진다. 하지만 정적 팩터리 메서드를 사용하면 컴퍼일러가 형인자를 스스로 알아내도록 할 수 있다.  이런 기법을 *자료형 유추(type inference)*라고 부른다.

### 단점
1. public이나 protected로 선언된 생성자가 없으므로 하위 클래스를 만들 수 없다.
2. 정적 팩터리 메서드가 다른 정적 메서드와 확연히 구분되지 않는다. 
    - 생성자와는 달리 정적 팩터리 메서드는 구별이 쉽지 않다. 주석을 통해 알리거나 이름을 지을 때 조심할 수 밖에 없다. 보통 다음과같은 이름을 사용한다.
        - valueOf
        - of
        - getInstance
        - newInstance
        - getType
        - newType

## 정리
정적 팩터리 메서드와 public 생성자는 용도가 서로 다르며 그 차이와 장단점을 이해하는 것이 중요하다. 정적 팩터리 메서드가 효과적인 경우가 많으니, 정적 팩터리 메서드를 고려해 보지도 않고 무조건 public 생성자를 만다는 것은 삼가기 바란다.



---
# ?
계승(inheritance)과 구성(Composition)
