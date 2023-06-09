### 흐름 제어 기법이 사용되는 이유

- `송신 측`과 `수신 측`의 데이터 처리 속도 차이를 해결하기 위해서

- 송신 측의 데이터 처리 속도가 수신 측보다 빠를 경우
  
  - 수신 측에서 제한된 저장 용량을 초과한 이후에 도착하는 데이터는 손실 될 수 있으며, 만약 손실 된다면 불필요하게 응답과 데이터 전송이 송/수신 측 간에 빈번이 발생

- 주요 기법
  
    ![흐름제어기법](./image/%ED%9D%90%EB%A6%84%EC%A0%9C%EC%96%B4%EA%B8%B0%EB%B2%95.png)
  
  - stop and wait
    
    - 과정
      
      1. 송신자는 데이터 프레임을 전송하고, 수신자는 해당 프레임을 수신한 후 응답(ACK 또는 NACK)을 송신자에게 보냄
      
      2. 송신자는 응답을 받은 후 다음 데이터 프레임을 전송
         
         1. 수신자가 프레임을 올바르게 수신하지 못했다면, 송신자는 이를 감지하고 해당 프레임을 재전송
      - 장점
        
        - 단순한 구조로 구현이 용이
        
        - 수신자의 응답을 받기 전까지는 송신자가 다음 데이터를 전송하지 않으므로 수신자의 처리 속도에 맞게 데이터를 전송할 수 있음
      
      - 단점
        
        - 송신자는 데이터의 응답을 기다리는 동안 아무 작업도 수행하지 않기 때문에 효율성이 떨어짐
        
        - 네트워크 지연이 발생할 경우 전체 처리 시간이 길어질 수 있음
  
  - sliding window
    
    - stop and wait에 비해 효율성을 향상시킨 흐름 제어 기법
    
    - 송신자와 수신자 간에 윈도우 크기만큼의 데이터 프레임을 전송하고, 송신자는 응답을 받지 않고도 윈도우 크기만큼의 추가 데이터를 전송할 수 있음
      
      - 윈도우 크기(window size)
        
        - 송신자와 수신자 사이에서 동시에 전송 가능한 데이터 프레임의 개수
    
    - 수신자는 정확하게 수신한 데이터 프레임을 응답(ACK)로 송신자에게 보내고, 송신자는 ACK를 받은 후 윈도우를 이동시켜 미확인 프레임을 재전송
    
    - 장점
      
      - 송신자가 응답을 기다리지 않고도 윈도우 크기만큼의 추가 데이터를 전송할 수 있으므로 전송 효율이 향상됨
      
      - 네트워크 대역폭을 효과적으로 활용할 수 있음
      
      - 수신자는 수신한 데이터 프레임을 순서대로 처리할 수 있으므로 복구 및 재전송 로직이 단순화됨
    
    - 단점
      
      - 구현이 복잡하고 오류 처리 로직이 필요
      
      - 정확한 윈도우 크기 설정이 중요하며, 크기가 너무 작으면 효율성이 떨어지고, 너무 크면 오버헤드가 발생할 수 있음
