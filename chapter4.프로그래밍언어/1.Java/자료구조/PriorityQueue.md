# 우선순위 큐(PriorityQueue)
- 일반적인 큐의 구조(FIFO)를 가지면서,
- 데이터가 들어온 순서대로 데이터가 나가는 것이 아닌 우선순위를 먼저 결정하고, **우선순위가 높은 데이터가 먼저 나가는 자료구조**!
  - 이 말은 즉, `PriorityQueue`를 사용하기 위해선 우선순위를 정해줘야하는데,  그것을  `Comparable` 인터페이스로 구현해줄 수 있다.
  - comparable에 관해서는 이미 언급한 바에 있으니, 링크를 참조하자 [Comparable](../문법/Comparable인터페이스.md)
- `PriorityQueue`는 자료구조 `Heap`을 이용하여 구현된다   

그럼 먼저 Heap 자료구조에 대해 알아보자
