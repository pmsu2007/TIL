# @WebMvcTest

`@WebMvcTest`는 <u>**컨트롤러 계층만 슬라이스 테스트할 수 있도록 돕는 어노테이션**</u>이다.

`@WebMvcTest`는 웹 계층과 관련된 빈(Bean)들만 찾아서 등록한다. 일반적인 `@Component`나 `@ConfigurationProperties` 등을 사용하는 빈들은 등록되지 않는다.

또한, `@WebMvcTest`는 Spring Security와 `MockMvc`를 자동으로 구성한다.
`MockMvc`를 더 세밀하게 제어하고 싶다면 `@AutoConfigureMockMvc` 어노테이션을 사용할 수 있다.

일반적으로 테스트하는 컨트롤러에 추가적인 빈(Bean)을 생성하기 위해서 `@MockBean`과 `@Import`를 조합하여 사용하기도 한다.

## 웹 계층과 관련된 빈(Bean)

- `@Controller`, `RestController`
- `@ControllerAdvice`, `@RestControllerAdvice`
- `@JsonComponent`
- `WebMvcConfigurer`
- `Filter`

## `@WebMvcTest`의 한계
스프링부트가 제공하는 테스트는 애플리케이션 컨텍스트를 구성한다. 

하지만 모든 테스트마다 애플리케이션 컨텍스트를 구성하는 것은 많은 비용을 요구하기 때문에 <u>**내부적으로 애플리케이션 컨텍스트를 캐싱해두고 동일한 설정이라면 재사용**</u>한다.

### 애플리케이션 컨텍스트 설정에 변경을 주는 기능
- `@MockBean`, `@SpyBean`
- `@TestPropertySource`
- `@ConditionalOnX`
- `@WebMvcTest`에 컨트롤러 지정
- `@Import` 
