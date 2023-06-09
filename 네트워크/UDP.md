### UDP (User Datagram Protocol)

> 전송계층에 속하는 프로토콜으로 **비연결지향** 프로토콜
> 
> 데이터그램 패킷 교환 방식 이용
> 
> 특징
> 
> - 비연결지향, 단방향 통신
>   
>   - 3 way handshake / 4 way handshake X
> 
> - TCP보다 신뢰성이 떨어지지만 전송 속도가 일반적으로 빠름
> 
> - 데이터의 순차 전송 보장 X
> 
> - 흐름 제어 X
> 
> - 혼잡 제어 X
> 
> 실시간 스트리밍, DNS 조회, 음성 및 영상 통화 등 비교적 데이터의 신뢰성이 중요하지 않고 신속한 데이터 전송이 중요한 경우 사용

---

- UDP
  
  - 데이터를 쪼개지 않고 UDP Header 붙임
    
    - 포트 번호를 이용해 전송
    
    - 데이터 단위
      
      - 데이터그램
  
  - 특징
    
    - 비연결 지향
      
      - 연결 설정 단계 없이 데이터를 전송
      
      - 각각의 데이터 그램은 독립적으로 처리
    
    - 단방향 통신
      
      - 수신자는 데이터를 받을 수 있지만, 송신자에게 응답을 보내지 않음
      
      - 양방향 통신이 필요한 경우 추가적인 구현이 필요
    
    - 비신뢰성
      
      - 데이터 전송을 보장하지 않아 데이터의 손실, 중복, 순서 변경 등이 발생할 수 있음
    
    - 속도와 간결성
      
      - TCP보다 속도가 빠르고, 처리량이 많은 환경에서 유리

- 데이터그램 패킷 교환 방식
  
  ![Untitled](./image/%EB%8D%B0%EC%9D%B4%ED%84%B0%EA%B7%B8%EB%9E%A8%ED%8C%A8%ED%82%B7%EA%B5%90%ED%99%98%EB%B0%A9%EC%8B%9D.png)
  
  - 데이터그램 패킷 교환 방식은 데이터를 작은 단위인 패킷으로 나누어 전송하는 방식
  
  - 데이터 전송 중에는 경로가 변경될 수 있으며, 각 패킷은 독립적으로 전송되므로 패킷 분실이나 손상이 발생할 수 있음
