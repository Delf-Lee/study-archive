# 우아한 테크코스 프리코스 1주차 과정 및 느낀점

## Google Java Style Guide
요구사항 중 **자바 코드 컨벤션**을 지키며 프로그래밍을 하라는 사항이 있었다. 겪어본 적은 없지만, 개발자에 따라 스타일이 제각각일 수 있고 (indentation, line break부터 시작해서 네이밍까지...) 경우에 따라서는 그 조직마다 이런 규약을 정해놓는다고 들었다.

> Google Java Style Guide  
> https://google.github.io/styleguide/javaguide.html

위 가이드를 따르는 것을 요구하는 것을 보니, 대중적이고 효율적인 규약들을 정리해 놓은 것 같았다.

대부분의 것들은 내가 지키고 있는 것 혹은 납득할만한 것이었는데, 한 가지 지키지 않고 있던 것이  있었다.

바로 `catch`문에서의 공백... [#](https://google.github.io/styleguide/javaguide.html#s4.1.3-braces-empty-blocks)

대표적으로 배열을 다룰 때, index validation을 일일히 하는것도 귀찮았고 다음과 같이 작성하는게 깔끔하다고 생각했다.
``` java
try {
    // 배열 접근 (ex. 2차원 배열에서 임의의 인덱스 기준으로 4방향 또는 8방향에 위치하는 인덱스에 접근)
} catch(ArrayIndexOutOfBoundsException e) {} // 상황에 따라 주석을 남김
```

찾아보니 허용되는 것 같다. [#](https://google.github.io/styleguide/javaguide.html#s6.2-caught-exceptions)

## 1차 전체 피드백으로 느낀 점
대부분은 납득하고 지키기 위해 신경쓰고 있는 부분이었다. 내가 신경을 덜 쓴 부분이나, 지키지 못한 부분은 아래와 같다.
###  불필요하게 공백 라인을 만들지 않는다.
지난 1주차 요구사항을 안내할 때, 컨벤션을 강조하며 [구글 스타일 가이드](https://google.github.io/styleguide/javaguide.html)와 [잘 정리된 포스팅](https://myeonguni.tistory.com/1596)을 소개를 보았다. 이 관련 포스팅에서 본 내용이 기억나는데,

> 한 줄을 띄우고 코드를 작성하면, 논리적으로 관계가 있는 코드들을 쉽게 구분할 수 있기 때문에 코드의 가독성(readability)을 향상시킨다. 

라는 부분이었다. 반대로 이 패드백은 너무 많은 공백 라인에 대한 경계를 상기시켜주었다. 사실 어떤 경우가 가독성을 높여주는지, 어떤 경우가 불필요한지 아직까지는 명확하게 판단할 수는 없지만, 확실히 조금 더 생각하게끔 해주는 피드백이었다.

### 의미 없는 주석을 달지 않는다.
**가장 뜨끔한 부분이었다.** 사실 이번 미션을 진행하면서 "더 보기 좋은", 또는 뭔가 "더 완벽해 보이는" 코드를 작성하기 위해 메서드 하나하나에 JavaDoc 주석을 달았다. 일일이 달면서 조금 피곤하기도 했고, 이렇게까지 해야하나 싶었는데 되돌아보니 조금 과했다는 생각이 든다. 내가 라이브러리를 만드는 것도 아닌데말이다!

앞으로는 되도록 조금 더 코드(클래스명, 메서드명, 변수명, 흐름)에 직관적으로, 명확하게 표현할 수 있도록 신경써야겠다.

### git commit 메시지를 의미있게 작성
정말 **항상** 느끼지만 어려운 부분이다. 어디까지가 "한 기능"인가에 대한 고민도 있지만, 구현하다보면 이것저것 작성해야 될것과 고쳐야할게 많이 보여서 일단 (까먹기 전에) 틀을 잡아놓는 습관이 있다. 사실 그런 코드들은 지금 내가 구현하고 있는 기능과에 대한 코드는 아니지만 근 시일 내에 구현해야할 관련된 코드이기는 하다.

이렇게 작성된 코드를 커밋하노라면 커밋 메시지와는 관련없는 부분이 포함되어 버리는 것이다. 그렇다고 기능의 범위를 조금 넓혀 나가면 커밋 단위가 너무 커져버린다.

아마 지금은 되도록 그 해당 기능만 구현하도록 신경쓰는 방법밖에 없을 듯 하다.
