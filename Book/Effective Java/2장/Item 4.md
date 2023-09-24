## 인스턴스화를 막으려거든 private 생성자를 사용하라

 객체 생성을 제한하기 위한 방법 중 하나로, 싱글톤패턴을 구현하는 방법을 다룬다.  
   
클래스의 인스턴스가 오직 하나만 생성되고, 어디서든지 그 인스턴스에 접근할 수 있도록 하고 싶을 때가 있다. 이런 요구사항을 만족시키려면 해당 클래스의 인스턴스 생성을
제한해야 한다. 제한하기 위해서 private 생성자를 사용하는 방법이 있다.

```
public class Singleton {
    private static final Singleton INSTANCE = new Singleton();

    private Singleton() {
        // private 생성자
    }

    public static Singleton getInstance() {
        return INSTANCE;
    }
}
```

위 코드에서 'Singleton' 클래스는 private 생성자를 가지고 있다. 이렇게 하면 클래스 외부에서 'new Singleton()'을 통한 인스턴스 생성이 불가능하다.  
대신, 'getInstace()'메서드를 통해 항상 같은 인스턴스를 반환하도록 설계되어 있다.  
  
이런 방식으로 private 생성자를 사용하여 객체의 인스턴스 생성을 제한함으로써, 싱글톤 패턴을 구현할 수 있다. 이렇게 하면 시스템 내에서 해당 클래스의 
유일한 인스턴스를 보장하고, 이를 통해 리소스 공유나 설정 정보와 같은 하나의 인스턴스만 필요한 경우에 사용할 수 있다.
