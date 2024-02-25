# Application.yml 설정 파일

```yaml
spring:
    # JPA 설정
    jpa:
        # 영속성 컨텍스트의 생명주기
        open-in-view: true
        hibernate:
            ddl-auto: update
            naming:
                physical-strategy: org.hibernate.boot.model.naming.CamelCaseToUnderscoresNamingStrategy
        use-new-id-generator-mappings: false
        
        properties:
            hibernate:
                # Hibernate가 DB에 수행하는 모든 쿼리문을 콘솔에 출력한다.
                show-sql: true
                format_sql: true
            dialect: org.hibernate.dialect.MySQL8InnoDBDialect
```
