## finalizer와 cleaner의 사용을 피하라

- Finalizer와 Cleaner  
Java에서는 객체가 더 이상 참조되지 않을 때, 가비지 컬렉션으로 해당 객체를 정리하는 메커니즘인 finalizer와 cleaner를 제공한다.
- Finalizer의 문제점  
Finalizer는 언제 실행될지 확신할 수 없고, 실행 시점이 예측 불가능하기 때문에 자원 해제에 사용하기 적합하지 않다. 또한 finalizer를 사용하면 성능 저하와 메모리 누수
문제가 발생할 수 있다.  
- Cleaner의 문제점  
Cleaner는 finalizer에 비해 개선도었다. 하지만 여전히 문제가 있어 사용하기 복잡하다.  
- 대신, 'try-with-resources' 문을 사용  
AutoCloseable 인터페이스를 구현한 객체를 활용하고, 수동으로 자원을 해제해야하는 경우 'close()' 메서드를 호출하여 명시적으로 장원을 해제하도록 해야 한다.
