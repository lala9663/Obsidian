## 아이템 14. Comparable을 구현할지 고려하라

**CompareTo** 는 자바에서 사용되는 메서드 중 하나로, 주로 객체 간의 비교를 수행하는데 활용된다. 
'compareTo' 메서드는 'comparable' 인터페이스에 정의되어 있으며, 객체를 정렬하거나 순서를 결정할 때 사용된다.

1. Comparable 인터페이스 
   - 자바에서 제공하는 인터페이스로, 객체의 정렬 순서를 지정하기 위해 사용된다.
   - compareTo 메서드를 구현하여 객체 간의 비교 로직을 정의한다.
2. 정렬 가능한 클래스로 만들기
   - 클래스를 정렬 가능한 클래스로 만들려면 Comparable 인터페이스를 구현하고 compareTo 메서드를 재정의해야 한다.
   - compareTo 메서드는 다른 객체와 현재 객체를 비교하고, 비교 결과에 따라 음수, 양수, 또는 0을 반환해야 한다.
3. compareTo 메서드 규칙
   - compareTo 메서드는 추이성, 반사성, 대칭성을 유지해야 한다.
   - 추이성: A.compareTo(B)가 양수이고, B.compareTo(C)가 양수이면, A.compareTo(C)도 양수여야 한다.
   - 반사성: 모든 객체 A에 대해 A.compareTo(A)는 항상 0 이여야 한다.
   - 대칭성: A.compareTo(B)가 양수이면 B.compareTo(A)는 음수여야 한다.
4. 비교 가능한 클래스의 이점
   - 비교 가능한 클래스를 사용하면 자바의 정렬 알고리즘(ex. Collections.sort)을 간편하게 활용할 수 있다.
   - 코드의 가독성이 향상되며, 정렬 관련 버그를 줄일 수 있다.
5. Comparable을 사용할 때 고려사항
   - compareTo 메서드에서 null 체크를 수행해야 한다.
   - compareTo 메서드에서 예외를 던지지 않아야 한다.
   - 상속 된계에서 compareTo의 규칙을 지켜야 한다.
6. Comparator를 사용해야 할 때
   - 이미 정의된 클래스나 라이브러리 클래스에 Comparable 인터페이스를 구현할 수 없는 경우, Comparable 인터페이스를 사용하여 별도의 비교자를 정의할 수 있다.

### 코드로 보기

```
public class Person implements Comparable<Person> {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public int getAge() {
        return age;
    }

    // compareTo 메서드를 구현
    @Override
    public int compareTo(Person otherPerson) {
        // 나이를 기준으로 비교
        return this.age - otherPerson.age;
    }

    @Override
    public String toString() {
        return "Person [name=" + name + ", age=" + age + "]";
    }
}

```


```
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

public class Main {
    public static void main(String[] args) {
        List<Person> people = new ArrayList<>();
        people.add(new Person("Alice", 30));
        people.add(new Person("Bob", 25));
        people.add(new Person("Charlie", 35));

        // 객체를 나이를 기준으로 정렬
        Collections.sort(people);

        for (Person person : people) {
            System.out.println(person);
        }
    }
}
```

```
Person [name=Bob, age=25]
Person [name=Alice, age=30]
Person [name=Charlie, age=35]
```