## 원형 (Prototype)

### 목적
원형이 되는(prototypical) 인스턴스를 사용하여 생성할 객체의 종류를 명시하고, 이렇게 만든 견본을 복사해서 새로운 객체를 생성

### 활용
- 제품의 생성, 복합, 표현 방법에 독립적인 제품을 만들고자 할 때
- 제품 클래스 계통과 병렬적으로 만드는 팩토리 클래스를 피하고 싶을 때
- 클래스의 인스턴스들이 서로 다른 상태 조합 중에 어느 하나일 때

### 이점
- object 생성에 높은 비용이 사용되는 경우 (DB에서 데이터를 가져오는 등) 원형 객체를 복사하여 비용을 줄일 수 있다
- 다른 생성패턴에 비해 클래스 수를 줄일 수 있다

### 단점
- 모든 제품에 clone 메서드 구현
- clone 메서드 구현시 주의사항
    - 언어에서 제공하는 복제 기능 사용 시 얕은 복사(shallow copy) 대 깊은 복사(deep copy) 문제 발생 가능
    - (일부 언어) 언어에서 제공하는 복제 기능 대신 복사 생성자 혹은 복사 팩토리 사용 권장
    
[복사 생성자/복사 팩토리 (자바 코드)]
```
public class Door extends MapSite {
    private Room room1;
    private Room room2;
    
    public Door(Room room1, Room room2) {
        this.room1 = room1;
        this.room2 = room2;
    }

    // 복사 생성자
    public Door(Door other) {
        this.room1 = other.room1;
        this.room2 = other.room2;
    }

    // 복사 팩토리
    public static Door newInstance(Door other) {
        return new Door(other.room1, other.room2);
    }
}
```

### 참고
 - [Python Design Patterns Tutorial - Prototype](https://www.tutorialspoint.com/python_design_patterns/python_design_patterns_prototype.htm)
 - [Java Prototype Pattern](https://blog.seotory.com/post/2015/09/java-prototype-pattern)
