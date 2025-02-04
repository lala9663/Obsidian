JPA N + 1 문제는 연관 관계가 설정된 엔티티를 조회할 경우에, 조회된 데이터 개수(N) 만큼 연관관계의 조회 쿼리가 추가로 발생한는 현상이다.  
예를 들어, 블로그 게시글과 댓글이 있는 경우, 게시글을 조회한 후 각 게시글마다 댓글을 조회하기 위한 추가 쿼리가 발생할 수 있다.  
이른 N + 1 문제라고 한다.  

### findAll 메서드의 글로벌 패치 전략 별 N + 1 문제 상황에 대한 설명  
(spring data jpa에서 제공하는 repository의 findAll 메서드)

글로벌 패치 전략을 즉시로딩으로 설정하고 findAll()을 실행하면 N + 1 문제가 발생한다.  
이는 findAll()은 select u from User u 라는 JPQL 구문을 생성해서 실행하기 때문이다.  
JPQL은 글로벌 패치 전략을 고려하지 않고 쿼리를 실행한다.  
모든 User를 조회하는 쿼리 실행 후, 즉시로딩 설정을 보고 연관관계에 있는 모든 엔티티를 조회하는 쿼리를 실행한다.  

글로벌 패치 전략을 지연 로딩으로 설정하고 findAll()을 실행하면 N + 1 문제가 발생하지 않는다.  
이는 연관관계에 있는 엔티티를 실제 객체 대신 프록시 객체로 생성하여 주입하기 때문이다.  
하지만 프록시 객체를 사용할 경우에 실제 데이터가 필요하여 조회하는 쿼리가 발생하고 N + 1문제가 발생할 수 있다.  

### 해결하는 방법

N + 1 문제를 해결하기 위해서는 fetch join, @EntityGraph를 사용해 볼 수 있다.  
fetch join은 연관 관계에 있는 엔티티를 한번에 즉시 로딩하는 구문이다.  
@EntityGraph도 비슷한 효과를 만들어내며, 쿼리 메서드에 해당 어노테이션을 추가해 사용할 수 있다.  

```
  select distinct u
  from User u
  left join fetch u.posts

  @EntityGraph(attributePaths = {"posts"}, type = EntityGraphType.FETCH)
  List<User> findAll();
```

----
- [JPA 모든 N+1 발생 케이스과 해결책](https://velog.io/@jinyoungchoi95/JPA-%EB%AA%A8%EB%93%A0-N1-%EB%B0%9C%EC%83%9D-%EC%BC%80%EC%9D%B4%EC%8A%A4%EA%B3%BC-%ED%95%B4%EA%B2%B0%EC%B1%85)
- [JPA Pagination, 그리고 N + 1 문제](https://tecoble.techcourse.co.kr/post/2021-07-26-jpa-pageable/)
