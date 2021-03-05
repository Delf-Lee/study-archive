# enum
enumerated type(열거형)이라고도 불리는 enum은 관련된 상수들의 모음이다.

## 기존의 상수 활용 방법
우리는 종종 어떤 의미 있는 데이터를 특정 값(상수)으로 치환하여 코드를 작성한다. 이를테면 다음과 같다.

``` java
static final int APPLE = 1;
static final int BANANA = 2;
static final int KIWI = 3;

public int getPrice(int fruit) {
    switch(fruit) {
        case APPLE: 
            return 1000;
        case BANANA:
            return 2000;
        case KIWI:
            return 3000;
    }
}
```
간단하고 편리하게 작성할 수 있지만 이런 방법은 여러가지 문제를 가지고 있다.

Java에서는 `Enum`이라는 클래스를 이용하여 열거형을 더욱 편리하게 다룰 수 있도록 도와준다.

## enum 정의하는 방법

Java에서 class를 정의하듯 작성하면 된다.

열거형의 명명은 클래스와 같이 첫글자만 대문자로 하는 카멜 표기법으로 작성한다. 또한 열거 타입의 상수 이름은 관례적으로 모두 대문자로 한다.

``` java
enum Fruite {
    APPLE, BANANA, KIWI;
}
```

## enum이 필요한 이유

위와 같이 정의함으로써 우리는 처음의 코드를 다음과 같이 다시 작성할 수 있다.

``` java
public int getPrice(Fruit fruit) {
    switch(fruit) {
        case Fruit.APPLE: 
            return 1000;
        case Fruit.BANANA:
            return 2000;
        case Fruit.KIWI:
            return 3000;
    }
}
```
...이게 뭐가 개선된거지? 라고 생각할 수 있다. 

일단 간단하게 요약한다면 코드가 **type safe**하게 변경되었다. 같은 표현으로 타입 안정성이 보장된다. 타입 세이프하다. 등등으로 표현할 수 있다.

기존의 코드에서는 다음과 같은 문제가 발생할 수 있다.

``` java
final static int APPLE = 1;
final static int BANANA = 2;
final static int KIWI = 3;
final static int ORANGE = 3; // KIWI에게 할당된 3이 또 할당됨
```

바보같다고 생각하는가? 이런 실수가 발생할 수 있는 것 자체가 type safe하지 않다는 것이다. 반면 enum을 이용하면 다음과 같이 변경하면 된다.

``` java
enum Fruite {
    APPLE, BANANA, KIWI, ORANGE;
}

public int getPrice(Fruit fruit) {
    switch(fruit) {
        case Fruit.APPLE: 
            return 1000;
        case Fruit.BANANA:
            return 2000;
        case Fruit.KIWI:
            return 3000;
        case Fruit.ORANGE:
            return 3500:
    }
}
```

다른 한가지 상황을 가정해서 상수들을 추가해보자.
```java
// 과일
final static int APPLE = 1;
final static int BANANA = 2;
final static int KIWI = 3;
// 회사
final static int APPLE = 1;
final static int SAMSUNG = 2;
```

위의 `APPLE`은 과일을 구분하기 위한 상수이고, 아래의 `APPLE`은 회사를 구분하기 위한 상수이지만, 이름이 같아서 변수명 충돌이 발생한다.

어쩔 수 없이 다음과 같이 변경하였다.
``` java
// 과일
final static int FRUIT_APPLE = 1; // 변수명 앞에 FRUITE 추가
final static int FRUIT_BANANA = 2;
final static int FRUIT_KIWI = 3;
// 회사
final static int COMPONY_APPLE = 1; // 변수명 앞에 COMPONY 추가
final static int COMPONY_SAMSUNG = 2;
```
해결된것 같지만 이런 문제도 발생할 수 있다.

아래의 코드는 어떻게 동작할까?
``` java
System.out.println(getPrice(COMPONY_APPLE)); // 1000
```

이 코드는?
``` java
System.out.println(FRUIT_APPLE == COMPONY_APPLE); // true
```
IT 기업의 가치가 1000원으로 폭락할 수도 있고, 과일 사과와 똑같이 취급될 수도 있다.

이 모든 문제는 위에서 말한 **타입 안정성**이 보장되지 않기에 일어날 수 있는 문제이다.

enum을 사용한다면 네임스페이스를 분리하여 이름의 충돌을 막을수도 있으며, 각 열거형 타입은 고유한 상수임이 보장된다.

``` java
enum Fruite {
    APPLE, BANANA, KIWI;
}

enum Compony {
    APPLE, SAMSUNG
}

System.out.println(Fruit.APPLE.equals(Compony.APPLE)); // false
System.out.println(Fruit.APPLE == Compony.APPLE); // 참고: 컴파일 에러 (비교 연산자로 비교할 수 없음)
```


클래스에서 필드를 선언하고 값을 할당하듯 enum의 각 타입에도 같은 일을 할 수 있다.

초기화는 다음과 같이 한다.

``` java
enum Fruite {
    APPLE(1000), BANANA(2000), KIWI(3000), ORANGE(3500); // 열거형 선언과 초기화
    
    int price; // 필드

    private Fruit(int price) { // 생성자
        this.price = price;
    }
}
```
`enum`의 생성자는 `private` 밖에 지정할 수 없다. 열거형 하나하나가 유일무이한 **상수**이기 때문에 외부에서 생성이 불가능하다.

이런 enum 특성을 이용해서 singleton 패턴을 구현하기도 한다.

## enum이 제공하는 메소드 (values()와 valueOf())
enum에서는 여러가지 메서드를 제공한다.

이렇게 메서드를 호출 할수 있는 이유는 사실 enum은 `java.lang.Enum`을 상속받은 클래스이기 때문이다. 우리가 작성한 코드는 컴파일떄 바이트 코드로 변환되면서 자동으로 `java.lang.Enum`을 상속받는다.

처음에 enum을 **관련된 상수의 모음**이라고 했는데, '열거'라는 단어에서 알 수 있다시피 enum에서 제공하는 메서드는 *순서가 있는*, 혹은 *연속된* 상수를 더 편리하게 표현하고 사용하는데 도움을 준다.

### `ordinal()`

`java.lang.Enum`에는 `ordinal`이라는 필드가 있고 이를 반환하는 메서드가 존재한다. 각 열거형 타입마다 선언된 순서에 따라 0부터 시작하는 정수를 할당 받는다.

``` java
enum Fruite {
    APPLE, BANANA, KIWI;
}

System.out.println(Fruit.APPLE.ordinal()); // 0
System.out.println(Fruit.BANANA.ordinal()); // 1
System.out.println(Fruit.KIWI.ordinal()); // 2
```
하지만, 실제 코드를 작성하는데 있어 개발자가 `ordinal()`을 쓸 일은 거의 없다. 오히려 지양해야하는 편.

enum을 변경하는 과정에서 어떤 타입이 (어디에) 추가되고 수정될지 모르기 때문에, 선언 순서(ordinal) 기반으로 코드를 작성한다면 코드 변경에 취약할 것이다.

#### ordinal과 JPA

JPA를 이용하여 Entity의 필드에 enum 타입이 있을 때,

``` java
enum Fruite {
    APPLE, BANANA, KIWI;
}

@Entity
class MyFavorite {
    @Id @GeneratedValue
    private Integer id;

    @Enumerated(EnumType.ORDINAL) // 아무것도 없으면 default 값
    private Fruit fruit;
}
```
이 `Fruit`는 ordinal 값이 저장되고, DB는 다음과 같을 것이다.
|id|fruit|비고|
|:-:|:-:|:-:|
|1 | 0 |사과|
|2 | 2 |키위|
|3 | 1 |바나나|

만약 추후에 변경사항이 생겨서 `Fruit`에 *이런식으로* 다른 타입이 추가된다면,

``` java
enum Fruite {
    GRAPE/* <- 추가됨 */, APPLE, BANANA, KIWI;
}
```
처음에 0으로 저장된 APPLE 꺼낼때 GRAPE가 되는 대참사가 벌어질 것이다.

|id|fruit|비고|
|:-:|:-:|:-:|
|1 | 0 |넣을땐 사과였지만 꺼낼땐 포도|
|2 | 2 |넣을땐 키위였지만 꺼낼땐 바나나|
|3 | 1 |넣을땐 바나나였지만 꺼낼땐 사과|

따라서 JPA에서 enum을 써야한다면  `@Enumerated(EnumType.ORDINAL)`이 아니라, `@Enumerated(EnumType.String)`을 사용하도록 하자.

한편 ordinal은 뒤에서 언급할 `EnumSet`이나 `EnumMap`에서 내부적으로 사용된다. (개인적으로 이걸 `ordinal()`메서드를 이용해서 굳이 밖으로 꺼내놓은 이유를 모르겠다)

### `valueOf()`
타입의 이름(문자열)를 주면 enum 인스턴스를 반환한다.

``` java
Fruit apple = Fruit.valueOf("APPLE");
```
대소문자를 구분하니 주의해야하자. (관례적으로 대문자로 통일하는 이유 중 하나가 아닐까)


### `values()`
선언된 모든 enum 인스턴스가 담긴 배열을 반환한다.

``` java
enum Fruite {
    APPLE, BANANA, KIWI;
}

for(Fruit f : Fruit.values()) {
    System.out.println(f);
}
```
``` console
APPLE
BANANA
KIWI
```
`valueOf()`와 `values()`는 모두 컴파일 타임에 리플렉션을 이용하여 생성되고 할당된다.

## `EnumSet`
`EnumSet`이라는 클래스는 enum의 모든 타입을 담긴 `Set`을 만들 수 있다.
``` java
EnumSet<Fruit> fruits = EnumSet.allOf(Fruit);
```

비슷하게 `EnumMap`이라는 클래스를 활용하여 `Map`을 만들 수도 있다.
```
EnumMap<Fruit, String> map = new EnumMap<>(Fruit.class);
```
사실 `HashMap`과 엄청난 차이가 있는건 아니다. `new EnumMap<>(Fruit.class)`이 반환하는건 어디까지나 빈 Map이고, element들은 직접 넣어줘야 한다.

`HashMap`보다 좋은 점은, `EnumMap`은 해싱에 내부 ordinal을 사용하므로 일반적인 해싱 알고리즘보다 빠르며, 크기가 정해져있기 때문에 resizeing으로 인한 성능저하가 없다.

### Reference
- https://wisdom-and-record.tistory.com/52
- https://www.notion.so/Enum-6ffa87530c424d8ab7a1b585bfb26fa2
- https://stackoverflow.com/questions/16980278/are-enummaps-in-java-perfect-hash-maps
- https://seungdols.tistory.com/464


---

처음껀 꼭 한번 봐라



@Enumerated(EnumType.ordinal) // ordinal 쓰면 안됨
(JAP 문맥)

바이트코드 잘 설명했어 // 1:01:00
values[]에 대하여

enumSet 정리 잘했어 // 1:05:00
