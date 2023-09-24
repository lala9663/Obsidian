## Private 생성자나 열거 타입으로 싱글턴임을 보증하라

**싱글턴** : 오직 하나만 생성할 수 있는 클래스

### 1. private 생성자와 public static 필드

```
public class Elvis {
    public static final Elvis INSTANCE = new Elvis();
    private Elvis { ... }
    public void leaveTheBuilding() { ... }
}
```

- 장점: 해당 클래스가 싱글턴임이 API에 명백히 드러난다. public static 필드가 final이니 절대로 다른 객체를 참조할 수 없다.
- 문제점:
  - 권한이 있는 클라이언트에서 리플렉션 API인 AccessibleObject.setAccessible을 사용해 private 생성자를 호출 할 수 있다.
  - 생성되는 시점을 조절할 수 있다.
  
### 2. private 생성자와 puvlic static 정적 팩토리 메서드

```
public class Elvis {
    private static final Elvis INSTANCE = new Elvis();
    private Elvis { ... }
    public static Elvis getInstance() {return INSTANCE;}
    
    public void leaveTheBuilding() { ... }
}
```
- 장점:  
  a. API를 바꾸지 않고도 싱글턴이 아니게 변경 가능하다.  
  b. 정적 팩터리를 제네릭 싱글턴 팩터리로 만들 수 있다.  
  c. 정적 팩터리의 메서드 참조를 공급자로 할 수 있다.  

   
### 3. 원소가 하나인 Enum 타입 선언
```
public enum Elvis {
    INSTANCE;
    public void leaveTheBuilding() { ... }
}
```

- 장점:
  - 간결하다.
  - 추가 노력 없이 직렬화 할 수 있다.
  - 아주 복잡한 직렬화 상황이나 리플렉션 공격에도 제2의 인스턴스가 생기는 일을 완벽히 막아준다.
- 문제점:
  - 싱글턴이 Enum 외의 클래스를 상속해야 하는 상황에선 불가능하다. 
