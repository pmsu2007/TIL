# NginX

NginX는 **비동기 이벤트 기반구조의 경량화 웹 서버**이다.

NginX는 클라이언트로부터 요청을 받았을 때 **요청에 맞는 정적 파일을 응답해주는 HTTP Web Server로 활용**되기도 하며, **Reverse Proxy Server로 활용하여 WAS의 부하를 줄일 수 있는 로드밸런서로 활용**되기도 한다.

NginX와 같은 웹 서버로 Apache가 있다. 이 둘은 요청을 처리함에 있어서
차이가 있는데, Apache의 경우 **요청마다 새로운 쓰레드를 생성하여 요청을 처리**하는데 반해 NginX는 **Event-Driven 구조로 동작**한다.

Apache의 경우 요청이 많으면 많을수록 자원이 많이 소모되고, NginX의 경우에는 하나 또는 고정된 개수의 프로세스를 사용하여 **요청을 Concurrency하게 처리하기 때문에 보다 적은 자원으로 운용이 가능**하다.

## NginX의 구조

![image](https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FbUefWi%2FbtrzUix8nEV%2Fk7IDvC3SjVYZbR5S3ekQkK%2Fimg.png)

NginX는 Master Process와 Worker Process로 구성되어 있다.

Master Process는 **NginX의 설정 파일을 읽고 해당 설정에 맞게 Worker Process를 생성**한다.

Worker Process는 **실제로 일을 하는 프로세스**이며, 생성될 때 지정된 Listen 소켓을 배정받는다.

해당 소켓에 대해 새로운 클라이언트의 요청이 들어오면 Connection을 형성하고 처리한다.

Connection은 정해진 Keep-Alive 시간만큼 유지되나, Connection이 형성되었다고 해서 Worker Process가 해당 Connection 하나만 담당하지 않는다.

즉, 형성된 Connection으로 부터 아무런 요청이 없다면 새로운 Connection을 형성하거나 이미 만들어진 Connection으로부터 들어온 요청을 처리한다.

이러한 Connection의 형성과 삭제, 새로운 요청을 처리하는 것을 이벤트(Event)라고 하며, 이 이벤트들은 OS 커널이 Queue 형식으로 Worker Process에게 전달한다.

Queue에 담긴 이벤트들은 비동기 상태로 대기하며, Worker Process는 하나의 스레드로 이벤트를 꺼내서 처리한다.

## 출처

- https://dkswnkk.tistory.com/513
