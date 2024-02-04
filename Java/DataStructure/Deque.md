# Deque (Double-Ended Queue)

덱(Deque)은 Double-Ended Queue의 줄임말로 <u>**큐의 양쪽으로 요소의 삽입과 삭제가 가능한 구조**</u>를 갖는다.

Java에서 Deque은 인터페이스이자 `Queue`를 상속하고 있으며, Deque의 구현체로는 `ArrayDeque`, `LinkedBlockingDeque`, `ConcurrentLinkedDeque`, `LinkedList`가 있다.

덱(Deque)은 `List` 인터페이스와 달리 인덱싱을 통한 접근을 제공하지 않는다.

## Deque 메소드

![alt text](https://github.com/pmsu2007/pmsu2007/assets/75938496/f1f55d08-0916-4e52-b88d-a0e7f7752ca9)

Deque 인터페이스는 <u>**Deque의 앞, 뒤에 있는 요소에 대해 삽입, 삭제, 요소 탐색을 하기 위한 메소드를 제공**</u>한다.

각 메소드는 두 가지 형태로 나뉘는데, 하나는 메소드의 수행이 실패하면 예외를 던지고 또 다른 하나는 메소드의 수행이 실패하면 `null` 이나 `false` 값을 반환한다.

## Deque 순회

```java
// for 문을 이용한 순회
Deque<E> dq = new ArrayDeque<>();

for (E elem : dq) {
  System.out.println(elem);
}

// Iterator를 이용한 순회
Iterator<E> iterator = dq.iterator();
while (iterator.hasNext()) {
  E elem = iterator.next();
  System.out.println(elem);
}

// 역순순회 
Iterator<E> reverseIterator = dq.descendingIterator();
while (reverseIterator.hasNext()) {
  E elem = reverseIterator.next();
  System.out.println(elem);
}
```