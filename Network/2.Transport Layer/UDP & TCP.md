#### 인터넷 애플리케이션에서 제공하는 두가지 프로토콜 UDP(User Datagram Protocol)과 TCP(Transmission Control Protocol)이 있다

애플리케이션 계층에서 내려온 데이터는 UDP 혹은 TCP 프로토콜의 헤더가 붙어 Segment로 만들어진다.

## 1\. User Datagram Protocol

-   비신뢰적, 비연결형이다.
-   데이터 패킷을 전송할 때 연결설정하는 과정 없이 바로 전송(TCP와 다르게 핸드쉐이킹 과정 없음) - **비연결형**
-   헤더에 최소한의 오류검출을 위한 체크섬필드가 존재. 그 이상 없음 - **비신뢰적**
-   흐름제어, 혼잡제어 없음
-   메시지가 제대로 전달되었는지 확인 안함
-   헤더의 길이는 32비트(8바이트) / TCP는 20바이트인것을 생각하면 패킷 오버헤드가 낮음

-   오버헤드가 낮기 때문에 실시간으로 데이터를 전송해야하는 애플리케이션(비디오 스트리밍, 게임, 인터넷 전화)에서 많이 사용
-   이들은 패킷손실이 조금있어도 동작에 큰 영향을 주지 않음
-   DNS는 UDP 사용하는 애플리케이션 계층 프로토콜

## 1-1. UDP 구조

| 출발지 포트 번호 | 목적지 포트 번호 |
| --- | --- |
| 길이 | 체크섬 |
| 애플리케이션 데이터 (메시지)                |  |

-   출발지 포트번호, 목적지 포트번호 : 다중화와 역다중화를 위해 사용된다
-   길이 : 길이를 통해서 다음 UDP 세그먼트의 시작 위치를 알 수 있다
-   체크섬 : 오류 검출을 도와준다.

## 2\. Transmission Control Protocol

-   UDP와 다르게 신뢰적, 연결지향형 서비스
-   혼잡제어, 흐름제어 가능
-   데이터의 순서를 보장한다
-   데이터를 보내기전에 3Way HandShaking을 통해 연결하기 때문에 연결지향형
-   데이터는 양방향으로 흐르기 때문에 전이중 서비스(full-duplex service)
-   단일 송신자와 단일 수신자의 연결이기에 point-to-point
-   UDP는 8바이트의 헤더를 갖지만, TCP는 20바이트의 헤더를 갖음

### 2-1. TCP 구조

| 출발지 포트번호 | 목적지 포트번호 |
| --- | --- |
| 순서번호 |  |
| 확인 응답 번호 |  |
| 헤더길이, 플래그필드 | 수신윈도 |
| 인터넷 체크섬 | 긴급 데이터 포인트 |
| 옵션 |  |
| 데이터 |  |

출발지, 목적지 포트번호 : 멀티플렉싱과 디멀티플렉싱에 사용

순서번호(SEQ), 확인응답번호(ACK): 신뢰적인 데이터 전송을 위한 필드. 

수신윈도: 흐름제어를 위해 사용되는 필드.
