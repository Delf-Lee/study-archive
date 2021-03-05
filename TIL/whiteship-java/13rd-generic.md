# 제네릭

제네릭(generic)이란 그 영어 단어에서 알 수 있다시피, 타입을 일반화(generalize)하여 사용할 수 있는 방법 혹은 그런 기능이다.



## 제네릭을 사용하는 이유
여러가지 사례를 들 수 있지만 모두 다음으로 귀결된다.

1. 타입 안정성(type safty)이 보장된다
2. 코드의 유지보수와 확장이 용이하다

## 제네릭 사용법
### 제네릭 클래스
우리가 자바에서 흔하게 접하는 자료구조인 `List`가 제네릭을 이용한 대표적인 클래스이다.

아래는 `List` 인터페이스의 일부를 간단하게 표현한 코드이다.
``` java
public interface List<E> {
    boolean add(E e);
    E get(int index);
}
```
이 인터페이스에서 쓸 타입을 `E` 라고 약속하고 코드를 작성한다. 예를들면 다음과 같다.
``` java
public E get(int index) {
    return (E) elementData[index]; // elementData는 Object의 배열
}
```

그리고 이 `E`는 외부에서 선언 시 타입을 정해주며, **컴파일 타임** 때 결정되어 동작한다.
``` java
List<String> list = new ArrayList<>();
```

### 제네릭 메서드
매개 변수에 제네릭 타입의 변수를 받은 메서드를 **제네릭 메서드**라고 한다.
제네릭 메서드를 정의하기 위해서는 반환 타입 앞에 사용할 제네릭 파라미터를 명시해줘야 한다.

다음은 `E`가 담긴 Collection 자료구조의 요소 개수를 카운팅해서 `Map`에 저장하는 메서드이다.
``` java
// (1): 사용할 제네릭 파라미터 명시
// (2): 반환 타입
public <E> Map<E, Integer> count(Collection<E> collection) {
//     ^^^ ^^^^^^^^^^^^^^^
//     (1)      (2)
    Map<E, Integer> map = new HashMap<>();
    for (E e : collection) {
    	map.merge(e, 1, Integer::sum);
    }
    return map;
}
```

### 제네릭 파라미터 이름
파라미터의 이름은 관례적으로 `E`, `T`, `K`, `V` 등이 사용된다.
- `E` - Element
- `T` - Type
- `K` - Key
- `V` - Value
  
### Bounded Type Parameters

위에서 사용한 것 처럼 제네릭 타입에 아무 제한도 주지 않는 것을 정규 타입 매개변수(`E`)라고 한다.

하지만 정규 타입 매개변수는 그저 저장하고 꺼낼 수 있다 뿐이지 연산이 불가능하다. 특정한 연산을 하려면 행위가 정의되어 있는 인터페이스로 타입 캐스팅을 해야하는데, 섣불리 타입 캐스팅을 했다가는 타입 안성성이 깨지게 된다.

여기 두개의 `Collection`을 인자로 받아 합쳐서 리스트로 반환하는 메서드가 있다. 정규 타입 매개변수만을 사용해서 구현한다면 다음과 같은 모습일 것이다.
``` java
public <E, T1, T2> Collection<E> concatCollectionToList(T1 t1, T2 t2) {
    Collection c1 = (Collection) t1;
    Collection c2 = (Collection) t2;

    List<E> list = new ArrayList<>();
    list.addAll(c1);
    list.addAll(c2);
    
    return list;
}
```
분명 컴파일이 되는 코드이지만 문제가 있다.

메서드 사용자가 이 메서드의 인자로 무엇을 넣을지 모른다. 예를들어 하나는 `List<String>`, 또 하나는 `List<Integer>` 을 넣어준다면 두 타입이 혼재되어 언제 런타임 에러를 일으킬지 모르는 `Collection`이 탄생하는 것이다.

심지어 `Collection` 조차 넣어주지 않을 가능성도 있다. 이땐 타입 캐스팅 부분부터 에러가 발생할 것이다.

타입 안정성을 위해 제네릭 매개변수의 타입을 제한할 필요가 있고, 이런 때를 위해서 **한정적 타입 매개변수**가 존재한다.

한정적 타입 매개변수를 사용하여 위의 메서드를 변경하면 다음과 같을 것이다.
``` java
static public <E, T1 extends Collection<E>, T2 extends Collection<E>> Collection<E> concatCollectionToList2(T1 t1, T2 t2) {
    List<E> list = new ArrayList<>();
    list.addAll(t1);
    list.addAll(t2);
    return list;
}
```
정의부가 길어졌지만, 구현은 훨씬 직관적이고 깔끔하게 바뀌었다. 

`TX`이 `TX extends Collection<E>`로 변경됐다. 이는 매개변수로 받는 `TX`는 `E`를 담은 `Collection`으로 한정한다는 의미이다.

## Wildcard Type Parameter

## 제네릭 주요 개념 (바운디드 타입, 와일드 카드)
## 제네릭 메소드 만들기
## Erasure