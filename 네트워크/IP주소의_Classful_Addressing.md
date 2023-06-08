### Classful Addressing (클래스 기반 주소 지정)

- IPv4에서 IP 주소를 5개의 class로 나누어 배분하는 방식
  
  - binary notation / dotted-decimal notation
    
    ![Untitled](./image/classful%20addressing%20notation.png)
  
  - subnet mask
    
    ![Untitled](./image/classful%20addressing%20subnet%20mask.png)

- Classful Addressing
  
  - class A
    
    - octet
      
      - binary notation에서 first byte가 0으로 시작
      
      - dotted-decimal notation에서 first byte가 0이상 127이하
    
    - subnet mask
      
      - `255.0.0.0`
      
      - host의 개수에서 2를 제외하는 이유
        
        - 첫 번째 주소는 네트워크 구별 주소
        
        - 마지막 주소는 브로드캐스트용 주소
          
          - 네트워크에 속해 있는 모든 컴퓨터에 데이터를 보낼 때 사용
  
  - class B
    
    - octet
      
      - binary notation에서 first byte가 10으로 시작
      
      - dotted-decimal notation에서 first byte가 128이상 191이하
    
    - subnet mask
      
      - `255.255.0.0`
  
  - class C
    
    - octet
      
      - binary notation에서 first byte가 110으로 시작
      
      - dotted-decimal notation에서 first byte가 192이상 223이하
    
    - subnet mask
      
      - `255.255.255.0`
  
  - class D
    
    - octet
      
      - binary notation에서 first byte가 1110으로 시작
      
      - dotted-decimal notation에서 first byte가 224이상 239이하
    
    - multicast
  
  - class E
    
    - octet
      
      - binary notation에서 first byte가 1111으로 시작
      
      - dotted-decimal notation에서 first byte가 224이상 255이하
    
    - 예비용

- 이해했는지 확인하기
  
  - IP Address를 통해 Class 찾기
    
      `192.168.1.10` -> C
    
      `10.10.200.6` -> A
    
      `172.15.165.1` -> B
    
      `230.10.65.30` -> D
  
  - subnet mask가 주어질 때 네트워크 주소가 일치하는지 확인하기
    
    - 네트워크 주소가 일치하면 switch를 통해 접근 가능
    
    - 네트워크 주소가 일치하지 않으면 router를 이용해야 함
      
      - `10.10.10.1`와 `10.10.20.16`
