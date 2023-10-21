
자바에는 기본형(Primitive) 타입과 참조형(Reference) 타입이 있다. 
일반적인 분류이다.

```
Java Data Type 
ㄴ Primitive Type
    ㄴ Boolean Type(boolean)
    ㄴ Numeric Type
        ㄴ Integral Type
            ㄴ Integer Type(short, int, long)
            ㄴ Floating Point Type(float, double)
        ㄴ Character Type(char)
ㄴ Reference Type
    ㄴ Class Type
    ㄴ Interface Type
    ㄴ Array Type
    ㄴ Enum Type
    ㄴ etc.
```


### Primitive type

- Java에서는 총 8가지의 Primitive type을 미리 정의하고 제공한다.
- 자바에서 기본 자료형은 반드시 사용하기 전에 선언되어야 한다.
- OS에 따라 자료형의 길이가 변하지 않는다.
- **비객체** 타입이라 null 값을 가질 수 없다. 만약 Null을 넣고 싶다면 Wrapper Class를 활용해야 한다.
- 스택(Stack) 메모리에 저장된다.

boolean, char, byte, short, int, long, float, double

### Reference type

- Java에서 Primitive type을 제외한 타입들이 모두 Reference type이다.
- Reference type은 Java에서 최상인 java.lang.Object클래스를 상속하는 모든 클래스를 말한다.
- 물론 new로 인하여 생성하는 것들은 메모리 영역인 Heap 영역에 생성을 하게되고, GC가 돌면서 메모리를 해제한다.
- 타입에는 class, interface, array, enum 타입이 있다.
- 빈 객체를 의미하는 Null이 존재한다.

#### String Class

클래스형에서도 String 클래스는 조금 특별하다. 이 클래스는 참조형에 속하지만 기본적인 사용은 기본형처럼 사용한다. 그리고 **불변**객체이다.