## 불필요한 객체 생성을 피해라

- 박싱된 기본 타입보다는 기본 타입을 사용하고, 의도치 않은 오토박싱이 숨어들지 않도록 주의하자.
  
```
// 예시1 - 문자열 생성
String myId1 = "MadPlay";
String myId2 = "MadPlay";
System.out.println(myId1 == myId2); // true

// 예시2 - 생성자로 문자열 생성 
String myId3 = new String("MadPlay");
String myId4 = new String("MadPlay");
System.out.println(myId3 == myId4); // false
```

- Auto-Boxing의 잘못된 예  
Auto-Boxing을 할 때 주의해야되는 점 중 하나는 Wrapper Class는 Auto Boxing 후 캐싱을 하더라도 새로운 값에 대해서는 계속 새로운 인스턴스를 만든다는 것이다.

```
private static long sum(){
    Long sum = 0L;
    for(long i = 0; i <= Integer.MAX_VALUE; i++){
        sum+=i;
    }
    return sum;
}
```

이 때 sum을 long이 아닌 wrapper class Long으로 한 것에 대한 실행 속도 차이는 10배라고 한다(Long으로 했을 때 10배 느리다).   

Long에 long을 더하는 행위는 AutoBoxing이 발생하고 매번 기존 값보다 큰 값으로 sum이 바뀌므로 sum은 Integer.MAX_VALUE만큼의 새로운 인스턴스가 생긴다.  

primitive type으로만 할 수 있을 때는 무조건 AutoBoxing을 피해야 한다.  
- 객체 생성은 무조건 비싸니 피해야 하는것은 아니다. 프로그램의 명확성, 간결성, 기능을 위해 객체를 추가로 생성하는 것은 일반적으로 좋다.
- 데이터베이스 연결 같은 생성 비용이 매우 비싼 경우가 아니라면 객체 풀을 만들지 말자. 일반적으로 자체 객체 풀은 코드를 헷갈리게 만들고, 사용량을 늘리고, 성능을 떨어뜨린다.
- 똑같은 기능의 객체를 매번 사용하기보다 객체 하나를 재사용하는 편이 나을 때가 많다. 재사용은 빠르다. 특히 불변 객체는 언제든 재사용할 수 있다.
- 생성자 대신 정적 팩터리 메서드를 제공하는 불변 클래스에서는 불필요한 객체 생성을 피할 수 있다.  
ex) Boolean(String) 생성자 대신 Boolean.valueOf(String) 팩터리 메서드를 사용하는 것이 좋다.  
