# Comparable<T> 인터페이스
Comparable 인터페이스는 **객체를 정렬**하는 데 사용되는 메소드인 **compareTo() 메소드를 정의**하고 있습니다.   
자바에서 같은 타입의 인스턴스를 서로 비교해야만 하는 클래스들은 모두 Comparable 인터페이스를 구현하고 있습니다.

- Boolean을 제외한 래퍼 클래스나 String, Time, Date와 같은 클래스의 인스턴스는 모두 정렬 가능합니다.
- 이때 기본 정렬 순서는 작은 값에서 큰 값으로 정렬되는 오름차순이 됩니다.
  
### 예시
	
-  Car.java
	
  ```
  public class Car implements Comparable<Car> {
	private String modelName;
	private int modelYear;
	private String color;

	Car(String mn, int my, String c) {
		this.modelName = mn;
		this.modelYear = my;
		this.color = c;
	}

	public String getModel() {
		return this.modelYear + "식 " + this.modelName + " " + this.color;
	}

	@Override
	public int compareTo(Car o) {
		if(this.modelYear == o.modelYear) {
			return 0 ;
		}
		else if(this.modelYear < o.modelYear ) {
			return -1;
		}
		else {
			return 1;
		}
	}
}
```
- Comparable01.java
						    
```
 public class Comparable01 {

    public static void main(String[] args) {

        Car car01 = new Car("아반떼", 2016, "노란색")
        Car car02 = new Car("소나타", 2010, "흰색");

        System.out.println(car01.compareTo(car02));  // 1출력
    }
}                                       
```                                    
- int comparaTo(T o) 단 하나의 추상메소드를 가지고 있다.
						    
						   
