## 팩토리 메서드 (Factory Method)

### 목적
객체를 생성하기 위한 인터페이스를 정의하지만, 어떤 클래스의 인스턴스를 생성할지에 대한 결정은 서브클래스에 위임한다

### 활용
- 어떤 클래스가 자신이 생성해야 하는 객체의 클래스를 예측할 수 없을 때
- 생성할 객체를 기술하는 책임을 자신의 서브클래스가 지정했으면 할 때
- 객체 생성의 책임을 몇 개의 보조 서브클래스 가운데 하나에게 위임하고, 어떤 서브클래스가 위임자인지에 대한 정보를 국소화시키고 싶을 때

### 이점
- 클라이언트 코드와 객체를 생성 하는 방법과 분리한다
- 시스템이 어떤 구체 클래스를 사용하는지에 대한 정보를 캡슐화한다
- 클라이언트 코드는 인터페이스와만 동작하기 때문에, 사용자가 정의한 어떤 서브클래스와도 동작할 수 있다

### 구현
1. 추상 클래스 정의: 추상 클래스(또는 인터페이스)로 정의하고, 서브클래스에서 정의한 팩토리 메서드를 대한 구현한다
2. 매개변수화: 팩토리 메서드가 매개변수를 받아서 어떤 종류의 제품을 생성할지 식별하게 만든다
    - JDK 사용 사례
       - java.util.Calendar#createCalendar()
       - java.text.NumberFormat#getInstance()

### 예제코드
##### 1. 추상 클래스 정의 예제
- [추상 클래스 코드](https://github.com/Hyunhoo-Kwon/DesignPatterens/blob/master/src/main/java/chapter03/factorymethod/MazeGame.java)
```
public abstract class MazeGame {
    public Maze createMaze() {
        // ...
    }
    // 팩토리 메서드들
    public abstract Room makeRoom(int n);
    public abstract Wall makeWall();
    public abstract Door makeDoor(Room r1, Room r2);
```

- [서브클래스 코드](https://github.com/Hyunhoo-Kwon/DesignPatterens/blob/master/src/main/java/chapter03/factorymethod/EnchantedMazeGame.java)
```
public class EnchantedMazeGame extends MazeGame {
    // 팩토리 메서드들
    @Override
    public Room makeRoom(int n) {
        return new EnchantedRoom(n);
    }
    @Override
    public Wall makeWall() {
        return new Wall();
    }
    @Override
    public Door makeDoor(Room r1, Room r2) {
        return new DoorNeedingSpell(r1, r2);
    }
}
```

- [호출 테스트 코드](https://github.com/Hyunhoo-Kwon/DesignPatterens/blob/master/src/test/java/chapter03/factorymethod/MazeGameTest.java)
```
@Test
public void createEnchantedMaze() throws Exception {
    MazeGame mazeGame = new EnchantedMazeGame();
    Maze maze = mazeGame.createMaze();
}
```

##### 2. 매개변수화 예제 [(Ref. https://www.tutorialspoint.com/design_pattern/factory_pattern.htm)]
- 매개변수화된 팩토리 메서드 코드
```
public class ShapeFactory {
   public Shape getShape(String shapeType){
      if(shapeType.equalsIgnoreCase("CIRCLE"))   return new Circle();
      else if(shapeType.equalsIgnoreCase("RECTANGLE"))  return new Rectangle();
      else if(shapeType.equalsIgnoreCase("SQUARE"))  return new Square();
      return null;
   }
}
```

- 호출 코드
```
public static void main(String[] args) {
      ShapeFactory shapeFactory = new ShapeFactory();
      Shape shape1 = shapeFactory.getShape("CIRCLE");
      Shape shape2 = shapeFactory.getShape("RECTANGLE");
      Shape shape3 = shapeFactory.getShape("SQUARE");
   }
```

### 단점
- 제품 클래스가 바뀔 때마다 새로운 서브클래스를 생성해야 한다
- 서브 클래스가 너무 많이 만들어진다

### 참고
 - [Design Patterns Tutorial - Factory Pattern](https://www.tutorialspoint.com/design_pattern/factory_pattern.htm)
