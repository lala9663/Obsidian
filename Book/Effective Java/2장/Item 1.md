## 생성자 대신 정적 팩터리 메서드를 고려하라

### 장점

### 1. 이름을 가질 수 있다.
정적 팩터리는 이름만 잘 지으면 반환될 객체의 특성을 쉽게 묘사할 수 있다.  
한 클래스에 시그니처가 같은 생성자가 여러 개 필요할 것 같으면, 생성자를 정적 팩터리 메서드로 바꾸고 각각의 차이를 잘 드러내는 이름으로 하자.
```
public class Phone {
  private String brand;
  private int price;

  public static Phone buyApple(int price){
    return new Phone("apple", price);
  }

  public static Phone buySamsung(int price){
    return new Phone("samsung", price)
  }
```
  외부에서 호출 하는 방식보다 이와 같은 방식으로 호출 하는 것이 의미를 파악하기 쉽다.

### 2. 호출될 때마다 인스턴스를 새로 생성하지는 않아도 된다.  
**불변 클래스(immutable class)**는 인스턴스를 미리 만들어 놓거나 새로 생성한 인스턴스를 캐싱하여 재활용하는 식으로 불필요한 객체 생성을 막을 수 있다.  
(특히 생성 비용이 큰) 같은 객체가 자주 요청되는 상황이라면 성능을 상당히 끌어올려 준다.  
```
public class Phone {
  private String brand;

  private static final Phone apple = new Phone("iPhone14");
  private static final Phone samsung = new Phone("zFlip);

  public Phone(String brand) {
    this.brand = brand;
  }
  public static Phone getInstanceApple() {
    return apple;
  }
  public staic Phone getInstanceSamsung() {
    return samsung;
  }
}

Phone apple = Phone.getInstanceApple();
```
  싱글톤 패턴을 생각해보면 될 것 같다.  

### 3. 반환 타입의 하위 타입 객체를 반환할 수 있는 능력이 있다.  

반환할 객체의 클래스를 자유롭게 선택할 수 있게 하는 '엄청난 유연성' 을 나타낸다.  

```
public List<String> one() {
  return new ArrayList<String>();
}

public List<String> two() {
  return new Vector<String>();
}
```
이러한 선택은 클라이언트 코드에서 List<String> 인터페이스를 사용하므로, 클라이언트 코드는 실제로 어떤 구현이 반환되는지 알 필요가 없다.  
  
이러한 유연성은 코드를 확장하고 유지 관리하기에 유용하다.  
따라서 반환 타입의 하위 타입 객체를 반환할 수 있는 능력은 객체 지향 디자인에서 다형성과 추상화를 적극적으로 활용하는데 효과적이고, 코드의 유연성과 확장성을 높일 수 있다.

### 4. 입력 매개변수에 따라 매번 다른 클래스의 객체를 반환할 수 있다.

```
interface Volume {
    void volumeUp();
    void volumeDown();
    
    static Volume of(String type) {
        switch (type) {
            case "apple" : return new AppleVolume();
            case "samsung" : return new SamsungVolume();
        }
        return null;
    }
}

class AppleVolume implements Volume {
    @Override
    public void volumeUp() {}
    @Override
    public void volumeDown() {}
}

class SamsungVolume implements Volume {
    @Override
    public void channelUp() {}
    @Override
    public void channelDown() {}
}
``` 

### 5. 정적 팩토리 메소드 작성 시점에는 반환 객체의 클래스가 존재하지 않아도 된다.
- 이런 유연함은 **서비스 제공자 프레임워크**를 만드는 근간이 된다. ex)JDBC
- 제공자: 서비스의 구현체로 클라이언트에서 제공하는 역할을 프레임워크가 통제하여, 클라이언트의 구현체로부터 분리해준다.

### 단점
1. 상속을 하려면 public이나 protected 생성자가 필요하니 정적 팩터리 메서드만 제공하면 하위 클래스를 만들 수 없다.
	- 상속이 불가능한 클래스가 된다. 상속보다 컴포지션을 사용하도록 유도하고 불변타입으로 만들려면 이 제약을 지켜야 한다는 점에선 장점이 될 수 있다.
2. 정적 팩터리 메서드는 프로그래머가 찾기 어렵다.
	- API 문서를 잘 써두고, 메소드 이름도 널리 알려진 규약을 따라 지어야 한다.
