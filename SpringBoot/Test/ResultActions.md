# ResultActions

`MockMvc`를 통해 컨트롤러를 슬라이스 테스트하게 된다면, 다음과 같은 코드로 수행하게 된다.

```java
@Test
public void 컨트롤러_슬라이스_테스트() {
    mockMvc.peform(get("/person/1"))
        .andExpect(status.isOk())
        .andExpect(content().contentType(MediaType.APPLICATION_JSON))
        .andExpect(jsonPath("$.person.name").value("Jason"));
}
```

`ResultActions`는 `MockMvc`가 수행한 결과를 검증하는 데에 사용되는 인터페이스이다.

## ResultActions 메소드

`ResultActions`는 `andExpect()`, `andExpectAll()`, `andDo()`, `andReturn()` 으로 총 4 가지의 메소드로 구성되어 있다.

### andExpect()

```java
ResultActions andExpect(ResultMatcher matcher) throws Exception;
```

`andExpect()`는 `MockMvc`가 수행한 결과를 검증하는데 사용하는 메소드이다.

`andExpect()`의 가장 큰 특징은 자기 자신인 `ResultActions`를 반환한다. 그렇기 때문에 다음과 같이 `Chaining Pattern` 을 적용할 수 있다.

```java
@Test
public void 컨트롤러_슬라이스_테스트() {
    mockMvc.peform(get("/person/1"))
        .andExpect(status().isOk())
        .andExpect(content().contentType(MediaType.APPLICATION_JSON))
        .andExpect(jsonPath("$.person.name").value("Jason"));
}
```

여기서 주의 해야할 점은, 세 개의 `andExpect()`가 모두 검증에 실패했을 경우 모든 `andExpect()`에 대한 결과가 출력되는 것이 아닌 첫 번째 `andExpect()`에 대한 결과만 출력된다.

### andExpectAll()

앞서 봤던 `andExpect()`가 가지는 문제를 보완하는 메소드이다.

```java
default ResultActions andExpectAll(ResultMatcher... matchers) throws Exception {
    ExceptionCollector exceptionCollector = new ExceptionCollector();
    for (ResultMatcher matcher : matchers) {
        exceptionCollector.execute(() -> this.andExpect(matcher));
    }
    exceptionCollector.assertEmpty();
    return this;
}
```

`andExpectAll()`을 사용하면 하나 이상의 검증이 실패하더라도 모든 검증을 확인할 수 있게 보장하고 다음과 같이 사용한다.

```java
@Test
public void 컨트롤러_슬라이스_테스트() {
    mockMvc.peform(get("/person/1"))
        .andExpectAll(
            status().isOk(),
            content().contentType(MediaType.APPLICATION_JSON),
            jsonPath("$.person.name").value("Jason")
        );
}
```

## ResultMatcher

`andExpect()`, `andExpectAll()` 모두 `ResultMatcher`를 파라미터로 받는다.

`ResultMatcher`는 실행된 요청의 결과과 예측 값과 일치하는지 검증하는데 사용되는 인터페이스이다.

```java
public interface ResultMatcher {
    void match(MvcResult result) throws Exception;
}
```

스프링에서는 `ResultMatcher` 기반의 팩토리 클래스인 `MockMvcResultMatchers` 클래스를 지원하기 때문에 따로 `ResultMatcher`를 구현하지 않아도 된다.

## MockMvcResultMatchers

`MockMvcResultMatchers` 클래스는 `ResultMatcher` 기반의 팩토리 클래스이다.

대표적으로 `status()`, `jsonPath()`, `content()`, `header()` 등의 메소드들이 있다.

### StatusResultMatchers

`StatusResultMatchers`는 `MockMvcResultMatchers`의 `status()`를 호출했을 때 반환되는 값으로, HTTP 상태 코드를 검증하는데 사용된다.

### JsonPathResultMatchers

`JsonPathResultMatchers`는 `MockMvcResultMatchers`의 `jsonPath()`를 호출했을 때 반환되는 값으로, 표현식을 통해 응답에 대해 접근하고 검증하는데 사용된다.

| 표현식 |                            설명 |
| :----- | ------------------------------: |
| `$`    |           현재 노드를 의미한다. |
| `*`    | 모든 자식 필드에 대해 접근한다. |
| `.`    |           자식 필드에 접근한다. |
| `[]`   |      배열 요소에 대해 접근한다. |
| `@`    |           속성에 대해 접근한다. |

```java
// users라는 배열 중 첫 번째 인덱스의 name 속성에 접근
jsonPath("$.users[0].name");

// user라는 객체의 name 속성에 접근
jsonPath("$.user.@name");
```