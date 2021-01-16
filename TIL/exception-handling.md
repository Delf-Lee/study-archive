# 예외 처리(Execption handling)
### 예외?
> **예외(例外)**
> 일반적 규칙이나 정례에서 벗어나는 일.

자바 입장에서 자신이 상정한 상황이 있을 것이다. 
개발자의 로직 실수이든, 예상치 못한 입력이든(사실 이것도 개발자의 실수라고 볼 수 도 있지만), 하드웨어적인 문제이든

### 예외 처리

이러한걸 처리해주는 것

## Exception과 Error의 차이는?
![](https://www.nextree.co.kr/content/images/2021/01/Exception-Class.png)


### 자바가 제공하는 예외 계층 구조
![](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F6mIpB%2FbtqzKeEZj4d%2FikDdTx2sya0KhaIeHmjf01%2Fimg.jpg)

### checked exception과 unchecked exception

-|Checked Exception|Unchhecked Exception
---|---|---
처리 여부|처리 강제|자유
확인 시점|Compile time|Runtime
예외 발생시 트랜잭션 처리|roll-back 하지 않음|roll-back 함
대표적인 예외|*`RumtimeException`를 상속 받은 모든 클래스*를 제외한 모든 클래스|`RumtimeException`를 상속 받은 모든 클래스



## 자바에서 예외 처리 방법 (try, catch, throw, throws, finally)
### 예외 처리 방법
#### 1. 예외 복구
예외복구의 핵심은 예외가 발생하여도 애플리케이션은 정상적인 흐름으로 진행된다는 것이다. 

``` java
int maxretry = MAX_RETRY;
while(maxretry -- > 0) {
    try {
        // 예외가 발생할 가능성이 있는 시도
        return; // 작업성공시 리턴
    }
    catch (SomeException e) {
        // 로그 출력. 정해진 시간만큼 대기
    } 
    finally {
        // 리소스 반납 및 정리 작업
    }
}
throw new RetryFailedException(); // 최대 재시도 횟수를 넘기면 직접 예외 발생
```
위 코드는 재시도를 통해 예외를 복구하는 코드이다. 

이 예제는 네트워크가 환경이 좋지 않아서 서버에 접속이 안되는 상황의 시스템에 적용하면 효율 적이다. 예외가 발생하면 그 예외를 잡아서 일정 시간만큼 대기하고 다시 재시도를 반복한다. 그리고 최대 재시도 횟수를 넘기면 예외를 발생시킨다. 재시도를 통해 정상적인 흐름을 타게 한다거나, 예외가 발생하면 이를 미리 예측하여 다른 흐름으로 유도시키도록 구현하면 비록 예외가 발생하였어도 정상적으로 작업을 종료할 수 있을 것이다.

#### 2. 예외처리 회피
``` java
public void add() throws SQLException {
    ... // 구현 로직
}
```
간단해 보이지만 아주 신중해야하는 로직이다. 예외가 발생하면 throws를 통해 호출한쪽으로 예외를 던지고 그 처리를 회피하는 것이다. 하지만 무책임하게 던지는 것은 위험하다. 호출한 쪽에서 다시 예외를 받아 처리하도록 하거나, 해당 메소드에서 이 예외를 던지는 것이 최선의 방법이라는 확신이 있을 때만 사용해야 한다.

#### 3. 예외 전환
``` java
catch(SQLException e) {
   ...
   throw DuplicateUserIdException();
}
```

예외 전환은 위의 코드처럼 예외를 잡아서 다른 예외를 던지는 것이다. 호출한 쪽에서 예외를 받아서 처리할 때 좀 더 명확하게 인지할 수 있도록 돕기 위한 방법이다. 어떤 예외인지 분명해야 처리가 수월해지기 때문이다. 예를 들어 Checked Exception 중 복구가 불가능한 예외가 잡혔다면 이를 Unchecked Exception으로 전환하여서 다른 계층에서 일일이 예외를 선언할 필요가 없도록 할 수도 있다.