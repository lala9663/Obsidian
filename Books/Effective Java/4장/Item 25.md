## 톱레벨 클래스는 한 파일에 하나만 담아라

**소스 파일 하나에 톱레벨 클래스를 여러개 선언**해도 자바 컴파일러는 불평하지 않는다. 하지만 아무런 득이 없고, **심각한 위험**을 감수해야 하는 행위이다.

한 클래스를 여러 가지로 정의할 수 있으며, 그중 어느 것을 사용할지는 어느 소스파일을 먼저 컴파일하느냐에 따라 달라지기 떄문이다.

### 하나의 소스 파일에 두 개의 톱레벨 클래스가 정의된 예시

다른 톱레벨 클래스 2개 (Utensil, Dessert)를 참조하는 Main 클래스가 있다고 가정하다.

```
public class Main { public static void main(String[] args) { System.out.println(Utensil.NAME + Dessert.NAME); } }
```

Utensil과 Dessert 클래스는 Utensil.java라는 한 파일에 정의되어 있다고 가정하자.

```
class Utensil { static final String NAME = "pan"; } class Dessert { static final String NAME = "cake"; }
```

Main을 실행하면 pancake를 출력한다. 이때, 우연히 똑같은 두 클래스를 담은 Dessert.java라는 파일을 만들었다고 가정하자.

```
class Utensil { static final String NAME = "pot"; } class Dessert { static final String NAME = "pie"; }
```

운 좋게 **javac Main.java Desert.java 명령으로 컴파일**한다면 컴파일 오류가 나고, Utensil과 Dessert 클래스를 중복 정의헀다고 알려줄 것이다.

컴파일러는 가장 먼저 Main.java를 컴파일하고, 그 안에서 Utensil 참조를 만나면 Utensil.java 파일을 살펴 Utensil과 Dessert를 모두 찾아낼 것이다. 그런 다음 컴파일러가 두 번째 명령줄 인수로 넘어온 Dessert.java를 처리핳려 할 때 같은 클래스의 정의가 이미 있음을 알게 된다.

한편, **javac Main.java나 javac Main.java Utensil.java 명령으로 컴파일**하면 Dessert.java 파일을 작성하기 전처럼 pancake를 출력한다. 그러나 **javac Dessert.java Main.java 명령으로 컴파일**하면 potpie를 출력한다.

* **이 처럼 컴파일러에 어느 소스 파일을 먼저 건네느냐에 따라 동작이 달라지므로, 반드시 바로 잡아야할 문제다.**

#### 해결책1

· 톱레벨 클래스들을 서로 다른 소스 파일로 분리한다.

#### 해결책2

· 톱레벨 클래스를 한 파일에 담고 싶다면, 정적 멤버 클래스(아이템 24)를 사용하는 방법을 고민한다.

- 다른 클래스에 딸린 **부차적인 클래**스라면 정적 멤버 클래스로 만드는 쪽이 일반적으로 더 낫다.

- **읽기 좋고**, private으로 선언하면([[Item 15]]) **접근 범위도 최소로 관리**할 수 있기 때문이다.


```
public class Test { 
	public static void main(String[] args) { 
		System.out.println(Utensil.NAME + Dessert.NAME); 
	} 
	
	private static class Utensil {
		static final String NAME = "pan"; 
	} 

	private static class Dessert { 
		static final String NAME = "cake"; 
		} 
	}
```


### 정리

자바 컴파일러는 하나의 소스 파일을 컴파일할 때, 해당 파일에 포함된 모든 톱레벨 클래스를 개별적으로 컴파일한다.
따라서 하나의 파일에 여러 개의 톱레벨 클래스를 정의하면, 각 클래스마다 별도의 클래스 파일이 생성되며 코드의 가독성과 유지보수성이 저하될 수 있다.
또한, 톱레벨 클래스를 분리하여 개별 파일로 만들면, 각 파일의 이름을 클래스의 이름과 일치시킬 수 있어 코드의 가독성을 높일 수 있다. 또한, 버전 관리 시스템을 사용할 때도 개별 파일 단위로 추적이 용이하며, 파일 단위로 컴파일 및 배포할 수 있다.

따라서, item 25에서는 톱레벨 클래스는 한 파일에 하나만 담는 것을 권고하고 있다. 이를 통해 코드의 가독성과 유지보수성을 향상시킬 수 있다.