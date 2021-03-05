# Critical Path(임계 경로)
멀티스레드 환경, 동시성에 관련된 컨텍스트 외에도 많이 쓰이는 말.

오히려 다른 쪽에서 먼저 쓰였고 활발하게 쓰이는 것 같다. 대표적인 예가 소프트웨어 공학 쪽의 프로젝트 매니징

![](https://mblogthumb-phinf.pstatic.net/20120816_73/k97b1114_1345099440445vASg4_JPEG/CPM%B3%D7%C6%AE%BF%F6%C5%A9.JPG?type=w2)

그래프 상에서 시작 노드와 끝 노드 사이의 **최장 경로**를 말한다.

## critical path method
critical path method라는 용어에서 많이 보인다. 분류하자면 '스케쥴링 알고리즘'.

다른 경로의 작업이 지연되면 여지가 있지만, critical path가 지연되면 얄짤없이 전체 작업이 지연된다. 때문에 critical path를 찾아내서 잘 관리하는게 중요하다.

## 멀티스레드 환경에서 critial path
같은 맥락으로 쓰일 수 있다. 목적지 노드까지의 path들이 각 스레드에서 수행하는데 걸리는 시간이고, 이때 처리시간이 가장 큰 작업을 critical path라고 부를 수 있겠다.

작업을 path라는 부르는게 뭔가 어색했었는데 그래프에서 온 개념이라고 하니 납득됐다.

프로젝트 매니징과 같은 맥락으로 오래 걸리는 작업(critical path)에 신경쓰고, 이 부분을 효율적으로 개선한다면 작업 효율이 오른다.

### Refernece
- https://m.blog.naver.com/k97b1114/140165850486
- https://jeonyeohun.github.io/2020/05/08/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%9E%84%EA%B3%84%EA%B2%BD%EB%A1%9C(Critical-Path).html