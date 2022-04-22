# 배열과 리스트 
자바를 사용해서 코드를 작성하다보면, 자주 사용하게되는 자료구조가 배열과 리스트가 있다.    
둘다 데이터의 그룹으로 여러 데이터를 사용하거나 관리할 때 사용된다.    
그렇기때문에, 사용하는 문법에서 헤깔리는 경우가 종종 있는데, 이번 기회에 정리하면서 나아갈 예정이다.   


## 배열(Array)
- 고정된 크기를 갖는 같은 자료형의 원소들이 연속적인(논리적 저장 순서와 물리적 저장 순서가 일치하는)형태로 구성된 자료구조이다.
  - 처음 크기를 지정하면 변하지않는다. 
      - ex) 처음 크기를 10으로 지정했다면, 5개의 데이터만 저장하더라도 실제 크기는 10이다. 
  - 인덱스에 따라 값을 유지하고, 원소가 삭제되어도 빈자리가 남게되어 메모리 낭비가 발생한다.

- #### 인덱스 : 각 원소의 번호로 0부터 시작하며, 해당 원소에 접근할 수 있다.
  - 접근(조회) 및 수정이 빠르게 가능하다.   
- cache hit  가능성이 커져 성능에 큰 도움이 된다.
   - CPU가 참조하고자 하는 메모리가 캐시에 존재하고 있는 경우 cache hit가 발생
- 하지만, 삽입과 삭제를 하여 배열을 연속적인 형태 유지를 해야한다면 shift연산을 해야하므로 O(n)이 된다.


## 리스트(List)
- 위에 배열의 문제점을 해결하기 위해 만든 자료구조이다.
- 빈틈없는 데이터의 적재라는 장점을 가진다. 
  - 원소를 삭제해도 삭제된 뒤 원소로 빈틈없이 연속적으로 위치한다. 
- 리스트의 핵심은 원소들 간의 순서로 **순서가 있는 데이터의 모임**이다.
  - 다른 이름으로 시퀀스(Sequence)라고 부른다.
-  배열에서 인덱스는 유일무이한 식별자이지만, 리스트에서는 몇번 째 데이터인지 정도의 의미를 가진다. (get(int index))
-  빈 element는 허용치 않는다. 
-  기본적으로 순차성을 보장하지 못하기 떄문에 special locality 보장이 되지않아 cache hit가 어렵다.
  -  spacial locality : 프로그램 실행 시 접근하는 메모리 영역은 이미 접근이 이루어진 영역의 근처일 확률이 높다는 프로그램 성격 표현
- 언어별로 list지원하는 것이 다르다. 

|언어|지원내용|
|--|--|
|C| 리스트 지원 안함|
|Javascript|배열에 리스트기능이 포함되어 있음|
|Python|기본이 리스트이며, 배열을 지원안함|
|Java|배열과 리스트 모두 지원, ArrayList와 LinkedList로 나뉨|

- 배열은 compile time에 할당되는 정적메모리에 할당되고, 리스트는 새로운 Node가 추가되는 runtime에 할당되는 동적메모리에 할당
    - run time : 컴파일 과정을 마친 응용 프로그램이 사용자에 의해 실행될 때
    - compile time : 소스코드가 컴파일을 통해 기계어 코드로 변환되어 실행 가능한 프로그램이 되는 편집 과정 



<br></br>

# Collections 와 Arrays


## 서로 자료구조 변환 (Object타입)

### 1. Array -> List
1. Arrays.asList()
  - 이경우 , List의 값이 바뀌면, Array값도 같이 변한다.
  - 그렇기 때문에 만약, List의 길이를 추가하게되면, 길이가 고정인 Array가 에러가 발생하게 된다.
2. new ArrayList<>(Arrays.asList())
  - 그래서 새로운 주소값을 할당해줘서, 서로 독립적이게 만들어준다.
3. Collectors.toList()
  - Stream().collect(Collectors.toList());
  - stream을 활용한 변환방법이다.
 
### 2. List -> Array
1. toArray()
 - String타입의 List에서 Array로 변환하는 경우 가능하다.
```
List명.toArray(new String[배열의 크기]);
```

---
  위의 경우 둘다 String[]과 List<String>인 경우만 가능하다.      
  왜냐하면 문자열 배열과, 문자열리스트의 원소값은 String으로 동일하기 때문이다.     
  <p></p>
  하지만, int의 경우 int[] 와 List<Integer>가 되는데, 
  이 경우는 int[]의 원소는 데이터 타입이 int로 primitive 타입이지만,    
  List의 원소는 데이터 타입이 Integer로 Object타입이다.    
  그래서 위와 같은 방법으로는 변환할 수가 없다. 
<br></br>
  
### 1. primitive 타입 Array -> List
	
1. 반복문
 	- 위에서 언급에 알수 있듯이, int타입을 Integer로 바꿔주기만하면, 변환이 가능하다는 것이다. 
	 - 그래서 반복을 통해 변환할 수 잇다. 
  
```
List<Integer> intList = new ArrayList<>() ;
int[] intArr = {1,2,3};

for(int i : intArr) {
	intList.add(i); //자동으로 wrap해준다.
}

```

 	primitive타입은 Arrays.asList()를 사용할 수 없으나 반복문을 통해 변환할 수 있다.
2. Stream 사용
	- 반복문보다는 아마 실제론 Stream을 더 많이 사용할 것이다. 
```
int[] arr ={1, 2, 3}
List<Integer>	intList = Arrays.stream(intArr).boxed().collect(Collectors.toList());	
```
### 2. primitive 타입 List -> Array
1. 반복문 
  - 반대로도 반복문을 통해 변환해줄수 있지만, 그리 자주 사용되진 않는다. 

```
List<Integer> intList = new ArrayList<>();
intList.add(1);
intList.add(2);
intList.add(3);

int[] intArr = new int[intList.size()];

for (int i = 0; i < intArr.length; i++) {
	intArr[i] = intList.get(i);
}
System.out.println(Arrays.toString(intArr));
```
                                                     
                                                     
2. Stream 
```
                                                    
list.stream().mapToInt(Integer::intValue).toArray();     
list.stream().mapToInt(i -> i).toArray(); // 자동 Wrapper 작동
  
```
위와같이 stream에서 mapToInt를 사용하여 Object를 primitive타입으로 변환해주고 
  toArray()를 통하여 배열로 변환해줄 수 있다.

	
## 정렬(sort)메소드 
- 변환 만큼이나 헤깔리는 것이 해당 데이터 그룹을 정렬 할때 이다.
- 확실하게 헤깔리지 않을라면 명확히 짚고 넘어가야한다. 
### 오름차순 정렬
#### 배열일때에는 Arrays.sort()사용
#### 리스트일때에는 Collections.sort()사용

	
### 내림차순 정렬

#### 배열일때에는 Arrays.sort(,Collections.reverseOrder())사용
	- Arrays 에는 아쉽게도 내부적으로 내림차순 정렬하는 메소드를 가지고 있지않다. 
  - 그래서 Collections에서 불러와야한다. 
#### 리스트일때에는 Collections.reverse()사용	
	- reverse()도 가지고 있다.
  
추가적으로 두 객체간 비교가 필요할 때는 implements Comparable{} 을 선언하여 
  ComepareTO() 메소드를 설정해주면 가능하다.    
  [참고 링크](https://github.com/PanghoChao/BackendRoadMap/blob/30748e73bd3ad9ed1d879eea633c727121e4aef5/chapter4.%ED%94%84%EB%A1%9C%EA%B7%B8%EB%9E%98%EB%B0%8D%EC%96%B8%EC%96%B4/1.Java/%EB%AC%B8%EB%B2%95/Comparable%EC%9D%B8%ED%84%B0%ED%8E%98%EC%9D%B4%EC%8A%A4.md)
	
