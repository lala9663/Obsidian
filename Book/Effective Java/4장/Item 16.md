## public 클래스에서는 public 필드가 아닌 접근자 메서드를 사용하라

- 클래스의 데이터 필드에 직접 접근할 수 있으면 캡슐화의 이점을 제공하지 못한다. [[Item 16]]
- API를 수정하지 않고는 내부 표현을 바꿀 수 없고, 불변식을 보장할 수 없으며, 외부에서 필드에 접근할 때 부수 작업을 수행할 수도 없다.
- 클래스의 필드는 모두 private으로 바꾸고 public 접근자(getter)를 추가하자.
- 패키지 바깥에서 접근할 수 있는 클래스라면 접근자를 제공함으로써 클래스 내부 표현 방식을 언제든 바꿀 수 있는 유연성을 제공한다.
- 변경제어: 필드에 값을 설정할 때 추가적인 로직을 수행하거나 값을 제한하려는 경우, 설정자 메서드를 사용하여 이를 구현 할 수 있다.

ex)
```
public class Person {
    public String name; // public 필드 사용
    public int age;     // public 필드 사용
}
```

위 클래스는 데이터를 직접 접근할 수 있기 때문에 데이터의 무결성을 보장하기 어렵고, 클래스의 내부 구현을 변경하기 어렵다. 따라서 다음과 같이 접근자 메서드를 사용하는 것이 바람직하다.

```
public class Person {
    private String name;
    private int age;

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        if (age < 0) {
            throw new IllegalArgumentException("나이는 음수일 수 없습니다.");
        }
        this.age = age;
    }
}
```

### 노출 사례
- 자바 플랫폼 라이브러리에도 public 클래스의 필드를 직접 노출한 사례가 있다.
  java.aws.package 패키지의 Point와 **Dimenssion** 클래스로, 그 중 Dimenssion 클래스는 해당 문제로 심각한 성능 문제가 있다. [[Item 67]]
  