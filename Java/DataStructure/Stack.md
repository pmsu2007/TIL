# Stack

스택은 <u>**마지막에 저장한 데이터를 가장 먼저 꺼내게 되는, LIFO(Last In First Out) 구조**</u>를 갖는다.

Java의 Stack은 Vector 클래스를 상속받기 때문에 Thread-Safe한 특징을 가지고 있다.

## Stack 구현체

```java
import java.util.Stack;

public class Stack<E> extends Vector<E> {

    public E push(E item) {
        addElement(item);

        return item;
    }

    public synchronized E pop() {
        E       obj;
        int     len = size();

        obj = peek();
        removeElementAt(len - 1);

        return obj;
    }

    public synchronized E peek() {
        int     len = size();

        if (len == 0)
            throw new EmptyStackException();
        return elementAt(len - 1);
    }

    public boolean empty() {
        return size() == 0;
    }

    public synchronized int search(Object o) {
        int i = lastIndexOf(o);

        if (i >= 0) {
            return size() - i;
        }
        return -1;
    }

}
```

Java는 `java.util.Stack` 클래스를 통해 스택(Stack)을 제공한다.

대표적으로 `pop()`, `push()`, `peek()`, `empty()`, `search()` 등의 메소드를 제공한다.

## Stack 사용법

### Stack 요소 넣기

스택(Stack)에 요소를 넣기 위해서는 `push()` 메소드를 사용한다.

```java
public E push (E item);
```

### Stack 요소 꺼내기

스택(Stack)에 요소를 빼기 위해서는 `pop()` 메소드를 사용한다.

`pop()`은 <u>**스택(Stack) 최상단의 요소를 반환하고 제거**</u>한다.

만약, 스택(Stack)이 비어있을 경우 `EmptyStackException`이 발생한다.

```java
public synchronized E pop();
```

### Stack 최상단 요소 가져오기

스택(Stack)에 최상단 요소를 가져오기 위해서는 `peek()` 메소드를 사용한다.

`peek()`은 <u>**스택(Stack) 최상단의 요소를 가져오기만 할 뿐 제거하지는 않는다.**</u>

```java
public synchronized E peek();
```

만약, 스택(Stack)이 비어있을 경우 `EmptyStackException`이 발생한다.

### Stack이 비어있는지 확인

스택(Stack)이 비어있는지 확인하기 위해서는 `empty()` 메소드를 사용한다.

스택(Stack)이 비어있다면 `true`를 반환하고, 비어있지 않다면 `false`를 반환한다.

```java
public boolean empty();
```

### Stack 요소 위치 확인

스택(Stack)에 특정 요소가 존재하는지 확인하기 위해서는 `search()` 메소드를 사용한다.

스택(Stack)에 해당 요소가 존재하면 순서를 반환하고 존재하지 않는다면 `-1`을 반환한다.

```java
public synchronized int pop(Object o);
```

## Stack은 Deprecated 되었다.

Java에서 스택(Stack) 자료구조를 사용해야 할 때, `Stack` 보다는 `Deque`를 사용함을 권장한다.

왜냐하면, `Stack` 클래스 자체는 `Vector`를 상속 받아 구현되었기 때문이다.

`Vector` 클래스는 취약점이 많고, 상속으로 인한 부모 메서드 공유 문제 때문에 잘못된 사용을 할 수 있기 때문이다.