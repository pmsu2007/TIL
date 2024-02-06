# 꿀팁 저장소

[문자열을 이용한 숫자 이어붙이기](#문자열을-이용한-숫자-이어붙이기) 

## [문자열을 이용한 숫자 이어붙이기](#문자열을-이용한-숫자-이어붙이기) 
```java
int a = 30;
int b = 40;

String strA = String.valueOf(a);
String strB = String.valueOf(b);

int ab = Integer.parseInt(strA + strB);
int ba = Integer.parseInt(strB + strA);

System.out.println("ab = " + ab); // 3040
System.out.println("ba = " + ba); // 4030
```
