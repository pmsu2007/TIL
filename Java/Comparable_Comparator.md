# Comparable_ Comparator

`Comparable`과 `Comparator`는 **객체 간의 비교**를 위한 인터페이스이다.


따라서, `Comparable`과 `Comparator`를 사용하기 위해서는 <u>
**인터페이스 내에 선언된 메소드를 오버라이딩 해주어야 한다.**
</u>

### 왜 필요한가 ?

일반적으로 Java에서는 primitive type 은 기본 자료형이기 때문에 부등호를 통해서 쉽게 비교가 가능하다.

그러나, 사용자 정의 클래스의 경우 **어떤 기준에 따라 비교를 해야할 지 알 수 없기 때문에** 비교 기준을 정해주어야 한다.


## Comparable
```java
public interface Comparable<T> {
    public int compareTo(T o);
}
```
`Comparable`은 인터페이스에서도 볼 수 있듯이, <u>**자기 자신과 매개변수 객체를 비교**</u>할 때 사용한다.

### 사용법
```java
public class Word implements Comparable<Word> {
        String content;
        int step;
        
        public Word(String content, int step) {
            this.content = content;
            this.step = step;
        }
        
        public int compareTo(Word o) {
            // 비교 기준 구현
        }
    }
```

#### 비교 기준 구현
```java 
public int compareTo(Word o) {
    if (this.step > o.step) {
        return 1; // 양수를 반환하면 자리를 바꾼다고 생각하면 된다.
    } else if (this.step == o.step) {
        return 0; 
    } else if (this.step < o.step) {
        reutnr -1; // 0, 음수를 반환하면 자리를 그대로 유지한다고 생각하면 된다.
    }
}
```
위 코드를 간단하게 바꾸면 다음과 같다.
```java
// 오름차순 정렬, 최소 힙
public int compareTo(Word o) {
    return this.step - o.step; 
}

// 내림차순 정렬, 최대 힙
public int compareTo(Word o) {
    return o.step - this.step;
}
```

## Comparator
```java
public interface Comparator<T> {
    public int compare(T o1, T o2);
}
```
`Comparator`는 인터페이스에서도 볼 수 있듯이, 타입이 같은 두 개의 객체를 매개변수로 전달받아 비교할 때 사용한다.

이미 `Comparable` 인터페이스가 있지만, `Comparator`이 필요한 경우가 있다.

1. 정렬 대상 클래스의 코드를 수정할 수 없는 경우
2. 정렬 대상 클래스에 이미 정의된 `compareTo` 와 다른 기준으로 정렬하고 싶은 경우
3. 여러 정렬 기준을 적용하고 싶은 경우


### 사용법
```java
public class WordComparator implements Comparable<Word> {

        
        public int compare(Word o1, Word o2) {
            // 비교 기준 구현
        }
    }
```

#### 비교 기준 구현
```java 
// 오름차순 정렬
public int compareTo(Word o1, Word o2) {
    return o1.step - o2.step; 
}

// 내림차순 정렬
public int compareTo(Word o1, Word o2) {
    return o2.step - o1.step;
}

---
Collections.sort(array, Comparator); // 다음과 같이 사용
```