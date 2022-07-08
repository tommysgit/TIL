# 3 Way Handshake & 4 Way Handshake

## 3-way handshake

응용 계층을 통과하며 전송 계층에서 TCP프로토콜은 서버와 네트워크 연결이 필요한데 이 과정을 3-way handshake이라고 한다. TCP헤더의 SYN ACK가 사용된다.

<img src= "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2F4mrsq%2FbtrlqCqRGxk%2F9bkRaPIysKHWWD8rfZp2A1%2Fimg.png"/>

- 클라이언트가 서버에 포트와 SYN 플래그가 설정된 헤더를 붙여 보낸다.
- 해당 포트가 열려있는 서버는 패킷을 받고 ACK와 SYN 플래그가 설정된 헤더를 붙여 수락의 표시를 한다.
- 클라이언트는 해당 패킷을 받고 ACK플래그가 설정된 패킷을 보낸다.

### Tip

IP 계층 에서의 헤더 IP는 Private IP로 공유기를 거치면서 NAT작업을 통해 Public IP로 변환된다.

## 4-way handshake

응용 계층간의 클라이언트와 서버의 요청과 응답이 완료되면 TCP 프로토콜의 경우 연결을 종료해야 하는데 이 과정을 4-way handshake라고 한다. TCP헤더의 SYN FIN이 사용된다.

<img src= "https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FSVziN%2FbtrlhxZaGUk%2FpZ1PkXva56jBpj5BuweVYK%2Fimg.png"/>

- 자신의 패킷을 다 송신한 클라이언트가 연결 종료를 위해 FIN 플래그가 설정된 패킷을 송신
- 서버는 해당 패킷을 잘 받았다는 의미로 ACK 플래그가 설정된 패킷을 송신
- 서버는 아직 자신이 보내야할 데이터가 있다면 이어서 보낸다. (Time Wait)
- 서버가 보내야 할 패킷을 다 송신 했다면 연결 종료를 합의하는 FIN 플래그가 설정된 패킷을 송신
- 클라이언트는 확인의 의미로 ACK 플래그가 설정된 패킷을 송신

### TCP 문제점

- 데이터를 주고 받을 때 마다 매번 Connection을 연결하여 시간 손실
- 신뢰성 이라는 장점이 있지만 패킷을 조금만 손실 하여도 재전송