## 인터페이스는 타입을 정의하는 용도로만 사용해라

인터페이스는 자신을 구현한 클래스의 인스턴스를 참조할 수 있는 타입 역할로만 사용해야 한다.
클래스가 어떤 인터페이스를 구현한다는 것은 자신의 인스턴스로 무엇을 할 수 있는지를 클라이언트에 얘기해주는 것이다.

### 인터페이스를 지침에 맞지 않게 사용한 예시 - 상수 인터페이스

- 상수 인터페이스란 메서드 없이, 상수를 뜻하는 static final 필드로만 가득 찬 인터페이스 이다.
- 이 상수들을 사용하려는 클래스에서는 정규화된 이름(qualified name)을 쓰는 걸 피하고자 그 인터페이스를 구현한다.

```
public interface PhysicalConstants { 
	static final double AVOGADRO_NUMBER = 6.022_140_857e23; 
	static final double BOLTZMANN_CONSTANT = 1.380_648_52e-23;  
	static final double ELECTRON_MASS = 9.109_383_56e-31; 
}
```

- 클래스 내부에서 사용하는 상수는 외부 인터페이스가 아니라 **내부 구현**에 해당한다. 따라서 상수 인터페이스를 구현하는 것은 내부 구현을 클래스의 API로 노출하는 행위다.
- 클라이언트 코드가 내부 구현에 해당하는 이 상수들에 종속될 수 있다. 그래서 다음 릴리스에서 이 상수들을 더 쓰지 않게 되더라도 바이너리 호환성을 위해 여전히 상수 인터페이스를 구현할 수 있어야 한다.
- final이 아닌 클래스가 상수 인터페이스를 구현하면, 모든 하위 클래스의 이름 공간이 그 인터페이스가 정의한 상수들로 **오염**되어 버린다.

### 올바르게 상수를 공개하는 방법

- 특정 클래스나 인터페이스와 강하게 연결된 상수라면 그 클래스나 인터페이스 자체에 추가한다. ex) Integer와 Double에 선언된 MIN_VALUE, MAX_VALUE
- 열거 타입으로 나타내기 적합한 상수라면, 열거타입으로 만들어 공개한다.([[Item 34]])
- 인스턴스화 할 수 없는 유틸리티 클래스([[Item 4]])에 담아 공개할 수도 있다.

```
public interface PhysicalConstants { 
	
	private PhysicalConstants(){}; // 인스턴스화 방지
		
	static final double AVOGADRO_NUMBER = 6.022_140_857e23; 
	static final double BOLTZMANN_CONSTANT = 1.380_648_52e-23;  
	static final double ELECTRON_MASS = 9.109_383_56e-31; 
}
```