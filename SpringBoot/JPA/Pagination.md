# Pagination

사용자가 게시물 목록을 요청했을 때 데이터베이스에 있는 수천 개 이상의 데이터를 모두 조회하여 제공한다면 서버에 엄청난 부하가 걸리게 될 것이다.

또한, 이는 사용자로 하여금 게시글 목록을 한눈에 보기 어렵게하기도 한다.

Pagination을 적용함으로써 적당한 양의 데이터를 잘라서 조회하여 제공한다면 <u> **서버에 걸리는 부하를 줄일 수 있을 뿐 아니라, UX 측면에서도 이점**</u>이 있다.

## JPA의 Pagination API

DB 벤더에 따라 페이징을 처리하는 쿼리가 달라진다.

그러나, JPA의 Pagination API를 사용한다면 어떤 DB 사용하는지와 관계 없이 페이징 쿼리를 자동으로 생성할 수 있다.

```java
public interface PostRepository extends JpaRepository<Post, Long> {
    @Query("select p from Post p")
    Page<Post> findWithPagination(Pageable pageable);
}
```

위의 코드와 같이 `Pageable` 구현체를 쿼리 메서드의 파라미터로 전달해줌으로써 쿼리에 페이징을 동적으로 추가해줄 수 있다.

### `PageRequest`

`PageRequest`는 `Pageable` 인터페이스의 구현체이다.

`PageRequest`는 일반적으로 `page`, `size`, `sort` 총 세 가지로로 구성된다.

- `page` : 0부터 시작하며 페이지 번호를 의미한다.
- `size` : 한 페이지에 들어가는 항목의 갯수를 의미한다.
- `sort` : 정렬 방식을 의미하며, `null` 값 대신에 `Sort.unsorted()`가 사용된다.


