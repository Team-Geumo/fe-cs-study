# 3-way Handshaking과 4-way Handshaking

## TCP

- TCP 통신 과정에서 데이터를 전송하기 위해서는 연결 상태, 가상의 통신로를 확보해야 함
- 가상의 통신로를 확보하기 위해 3-way Handshake라는 과정을 거치게 됨

## TCP 헤더, 코드비트

- TCP 헤더 중에 6비트로 구성된 코드비트가 있음
- TCP의 연결 확립, 종료 과정에서 역할을 함

![Untitled](image/TCP%20%ED%97%A4%EB%8D%94%EC%99%80%20%EC%BD%94%EB%93%9C%EB%B9%84%ED%8A%B8.png)

- 초기값은 0, 활성화시 1로 바뀌어서 전송됨

## **TCP 3-way Handshake**

### 정의

- TCP/IP프로토콜을 이용해서 통신을 하는 응용프로그램이 데이터를 전송하기 전에 정확한 전송을 보장하기 위해 상대방 컴퓨터와 사전에 세션을 수립하는 과정
- 양쪽 모두 데이터를 전송할 준비가 되었다는 것을 보장하고, 실제로 데이 전달이 시작하기전에

한쪽이 다른 쪽이 준비되었다는 것을 알수 있도록 함

### **TCP 3-way Handshake 과정**

![Untitled](image/3-way%20Handshake.png)

1. A의 연결 요청
    - A 클라이언트는 B 서버에 접속을 요청하는 **SYN** 패킷을 보냄
    - 이때 A 클라이언트는 SYN 을 보내고 SYN/ACK 응답을 기다리는 **SYN_SENT** 상태
    - B 서버는 **Wait for Client** 상태
2. B의 A 요청 확인 + 연결 요청
    - B 서버는 SYN 요청을 받고 A 클라이언트에게 요청을 수락한다는 **ACK** 와 **SYN** flag 가 설정된 패킷을 발송
    - 이때 B 서버는 **SYN_RECEIVED** 상태
3. A의 B 요청 확인
    - A 클라이언트는 B 서버에게 **ACK**을 보내고 이후로부터는 연결이 이루어지고 데이터가 오가게 됨
    - 이때의 B 서버는 **ESTABLISHED** 상태

### **2. 4-way Handshaking**

### 정의

- 세션을 종료하기 위해 수행되는 절차

![Untitled](image/4-way%20Handshake.png)

### **TCP 4-way Handshaking 과정**

1. A의 연결 종료
    - A 클라이언트가 연결을 종료하겠다는 FIN플래그를 전송
    - 이때  **A클라이언트는  FIN-WAIT** 상태.
2. B의 A 종료 요청 확인
    - B서버는 FIN플래그를 받고, 일단 확인메시지 ACK 보내고 자신의 통신이 끝날때까지 기다림
    - 이때 **B 서버는 CLOSE_WAIT 상태**
3. B의 연결 종료
    - 연결을 종료할 준비가 되면, 연결해지를 위한 준비가 되었음을 알리기 위해  클라이언트에게 FIN플래그를 전송
    - 이때 B서버는 **LAST-ACK 상태**
4. A의 B 종료 요청 확인
    - A 클라이언트는 해지준비가 되었다는 ACK를 확인했다는 메시지를 보냄
    - A 클라이언트의 상태가 **TIME-WAIT** 으로 변경되고, 일정 시간 이후 **CLOSE** 상태로 변화함

## 정리

- TCP는 연결을 확립하기 위해서 TCP 헤더의 코드비트를 사용함
- 연결을 확립할 시 3-way Handshake라는 과정을 거치게 되고 그 과정에서 코드 비트의 SYN과 ACK를 주고받음
- 연결을 종료할 시 4-way Handshake라는 과정을 거치게 되고 그 과정에서 코드 비트의 FIN과 ACK를 주고받음