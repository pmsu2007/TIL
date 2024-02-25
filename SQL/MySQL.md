# MySQL

[ROUND](#Round)

[TRUNCATE](#Truncate)

[IFNULL](#ifnull)

[IF](#if)

[NULLIF](#nullif)

[다중정렬][#다중정렬]

## 수학

### [ROUND](#Round)

**숫자를 지정된 소수점 자릿수로 반올림하는 데 사용되는 SQL 함수**

```SQL
SELECT ROUND(반올림 할 숫자, 소수점 자릿수) FROM TABLE

ROUND(12.345, 1) = 12.3을 반환
ROUND(12.345, 0) = 12를 반환
ROUND(12.345, -1) = 10을 반환
```

### [TRUNCATE](#Truncate)

**숫자를 버릴 자릿수 아래로 버리는 데 사용되는 SQL 함수**

```SQL
SELECT TRUNCATE(버림 할 숫자, 소수점 자리수) FROM TABLE

TRUNCATE(12.345, 1) = 12.3을 반환
TRUNCATE(12.345, 1) = 12를 반환
TRUNCATE(12.345, -1) = 10을 반환
```

## NULL 처리

### [IFNULL](#ifnull)

**NULL 값을 치환하는 데 사용되는 SQL 함수**

```SQL
SELECT IFNULL(컬럼, NULL을 대체할 값) FROM TABLE

IFNULL(Column, 'NONE') => null 값을 NONE으로 치환
```

### [IF](#if)

**컬럼 값이 NULL인 경우 1을, NULL이 아니라면 2를 반환**

```SQL
SELECT IF(컬럼명 IS NULL, '1', '2') FROM TABLE
```

### [NULLIF](#nullif)

**조건이 true이라면 null을, false이라면 첫 번째 파라미터 값을 반환**

```SQL
SELECT NULLIF(1, 1) => NULL 반환
SELECT NULLIF(1, 2) => 1 반환
```

### [다중정렬](#다중정렬)

**ORDER BY 다중정렬을 할 때, 왼쪽부터 순차적으로 정렬되기 때문에 순서를 고려해야 한다.**

```SQL
ORDER BY col1 DESC, col2 ASC;
```

**col1 기준으로 내림차순 정렬을 한 후, col1이 같은 값에 한해서 col2를 오름차순 정렬을 한다.**

### [다중조건](#다중조건)

**WHERE 절에서 다중 조건 필터링을 해야할 때가 있는데, OR을 사용하여 처리할 수 있지만 IN을 사용하여 처리하면 훨씬 효율적이다.**

```SQL
// OR 사용
WHERE 카테고리 = '가구' or 카테고리 = '옷';

// IN 사용
WHERE 카테고리 IN ('가구', '옷'); 

```