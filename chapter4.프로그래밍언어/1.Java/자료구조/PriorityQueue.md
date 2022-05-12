# 우선순위 큐(PriorityQueue)
- 일반적인 큐의 구조(FIFO)를 가지면서,
- 데이터가 들어온 순서대로 데이터가 나가는 것이 아닌 우선순위를 먼저 결정하고, **우선순위가 높은 데이터가 먼저 나가는 자료구조**!
  - 이 말은 즉, `PriorityQueue`를 사용하기 위해선 우선순위를 정해줘야하는데,  그것을  `Comparable` 인터페이스로 구현해줄 수 있다.
  - comparable에 관해서는 이미 언급한 바에 있으니, 링크를 참조하자 [Comparable](../문법/Comparable인터페이스.md)
- `PriorityQueue`는 자료구조 `Heap`을 이용하여 구현된다. [힙 참고자료](./Heap.md)   


## 특징
 - 높은 우선순위의 요소를 먼저 꺼내서 처리하는 구조
 - 시간 복잡도는 힙과 큐를 합친 O(Nlogn) 이다. 
 - 우선순위를 중요시해야 하는 상황에서 주로 쓰인다. 
 - 특히, 주의해야할 사항이 있는데 우선순위 큐는 올림차순으로 설정하면, 가장 작은값부터 반환하고 내림차순으로 설정해야, 가장 큰값 부터 반환한다. 
    - 그 이유는, 큐 특성상 맨 앞에부터 값을 반환하기 때문에, 맨앞이 가장 작은건 올림차순이고, 맨앞이 가장 큰건 내림차순이다. 

### 선언
`import java.util.PriorityQueue` 로 해당 패키지를 불러와야한다.

1. `PriorityQueue<Integer> priorityQueue = new PriorityQueue<>();`  
    - 기본적으로 `PriorityQueue<>`클래스를 불러와 생성하면, **올림차순**으로 생성된다.
    - 반환되는 값은 가장 작은값이 나온다.
2. `PriorityQueue<Integer> priorityQueue = new PriorityQueue<>(Collections.reverseOrder());`
    - `Collections.reverseOrder()`의 메소드를 도움받아 **내림차순**으로 생성된다.
    - 반환되는 값이 가장 큰 값이 나온다.
3. 



### Priority Queue 메소드
내부적으로란 Heap이고, 자료구조형태는 Queue라서 그런지, Queue와 참조메소드는 동일하다.
- add(): 큐의 맨뒤에 값을 추가한다.  
    - 반환값은 boolean으로 성공하면 True, 실패하면 false를 반환한다.
- poll() : 큐의 맨앞에 있는 요소를 반환하고, 큐에서 해당 요소를 제거한다.
    - 만약 큐가 비어있으면 null을 반환 
- remove() : 인자에 아무런 값이 없으면 맨앞 요소를 삭제한다.
    - 인자로 Object값을 넣으면 해당 요소가 삭제된다. 
- peek() :  큐의 맨 앞에 있는 요소를 반환함.
- element() :  큐의 맨 앞에 있는 요소를 반환함. 하지만, peek()를 더 많이 사용!
- clear() : 큐안의 값을 다 제거한다.

### Priority Queue 복사하기, 초기화
