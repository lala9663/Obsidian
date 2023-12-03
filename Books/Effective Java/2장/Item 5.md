## 자원을 직접 명시하지 말고 의존 객체 주입을 사용하라

1. 중요한 점은 DI(Dependency Injection)이다.  
**DI**(의존 객체 주입): 클래스가 필요로 하는 자원을 직접 생성하거나 가져오지 말고, 외부에서 해당 자원을 주입받도록 한다. 이를 통해 객체 간의 결합도를 낮출 수 있다.  
  
2. 유연성 향상
의존 객체 주입을 사용하면 자원을 생성하는 방식을 변경하거나 다른 구현체로 교체하기가 훨씬 쉬워진다. 예를 들어, 인터페이스를 하용하여 의존성을 주입하면 다양한 구현체를
주입할 수 있고, 이를 통해 코드의 유연성과 재사용성을 향상시킬 수 있다.

3. 테스트 용이성
이에 따라 단위 테스트를 수행할 때 유용하다.
테스트에서는 가짜(mock)객체나 테스트용 객체를 주입하여 객체를 격리된 환경에서 테스트할 수 있다.
  
  
DI의 예시를 들어보자.  
  
1. 데이터베이스 연결 객체를 나타내는 인터페이스와 그 인터페이스를 구현한 클래스

```
// 데이터베이스 연결 인터페이스
public interface DatabaseConnection {
    void connect();
    void disconnect();
}

// 데이터베이스 연결 구현 클래스
public class MySqlConnection implements DatabaseConnection {
    @Override
    public void connect() {
        // MySQL 데이터베이스 연결 로직
        System.out.println("MySQL 데이터베이스에 연결됨.");
    }

    @Override
    public void disconnect() {
        // MySQL 데이터베이스 연결 해제 로직
        System.out.println("MySQL 데이터베이스 연결 해제됨.");
    }
}
```
  
2. 서비스 클래스에서 의존 객체 주입 사용  
   
```
public class MyService {
    private final DatabaseConnection databaseConnection;

    // 생성자를 통한 의존 객체 주입
    public MyService(DatabaseConnection databaseConnection) {
        this.databaseConnection = databaseConnection;
    }

    public void performDatabaseTask() {
        // 의존 객체(databaseConnection)를 사용하여 데이터베이스 작업 수행
        databaseConnection.connect();
        // 작업 수행 로직
        databaseConnection.disconnect();
    }
}
```
  
3. 애플리케이션에서 실제 의존 객체를 생성하고 주입  
   
```
public class Main {
    public static void main(String[] args) {
        // MySQL 데이터베이스 연결 객체를 생성
        DatabaseConnection mysqlConnection = new MySqlConnection();
        
        // 서비스 클래스에 의존 객체 주입
        MyService myService = new MyService(mysqlConnection);
        
        // 서비스 클래스를 사용하여 데이터베이스 작업 수행
        myService.performDatabaseTask();
    }
}
```
