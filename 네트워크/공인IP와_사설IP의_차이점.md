# 공인 IP와 사설 IP의 차이점

날짜: 2023년 6월 8일
상태: 네트워크
작성자: 진우 하

<aside>
💡 공인 IP와 사설 IP의 차이점

</aside>

## 공인 IP와 사설 IP의 차이점

> **공인 IP**
> 
- ISP (인터넷 서비스 공급자)가 제공하는 IP 주소
    - 공인 IP는 전세계에서 유일한 IP 주소를 갖는다.
    - 다른 PC로부터 접근이 가능하다.
    - 털리면 안 되는 IP

> **사설 IP**
> 
- 가정이나 회사 등에 할당된 네트워크
    - 로컬 IP, 가상 IP라고도 한다.
    - 백엔드 서버 올렸을 때 가장 기본적인 IP = 사설 IP의 사설 IP ⇒ 172.0.0.1
    - 사설IP 주소는 다음 3가지 주소대역으로 고정된다.
        - Class A : **10**.0.0.0 ~ **10**.255.255.255
        - Class B : **172.16**.0.0 ~ **172.31**.255.255
        - Class C : **192.168**.0.0 ~ **192.168**.255.255
    - 공유기의 IP를 기준으로 할당된다.

> 차이점
> 
> - 공인 IP가 더 큰 개념. 공인 IP의 일부 주소에서 사설 IP를 할당해주는 식으로 사설망이 이루어진다.
> - 공인 IP는 외부에서의 접근이 가능하지만 사설 IP는 외부에서의 접근이 불가능하다.

---

### TMI

- VPN에 대하여.
    - VPN (Virtual Private Network)은 인터넷을 통해 안전한 개인적인 연결을 제공하는 기술이다.
    - VPN을 사용하여 데이터를 암호화, 인터넷 트래픽을 안전하게 전송하는 등 사용자의 신원을 숨길 수 있다.
    - VPN은 일반적으로 공인 IP 주소를 사용하여 작동한다.
        - VPN 사용자의 장치에서 인터넷으로 나가는 트래픽(사설 IP가 담겨있음)을 VPN 서버로 보낸다. VPN서버에서 해당 트래픽을 암호화하여(공인 IP로 대체하는 등의 방법) 인터넷으로 전달해준다.
        - 이 과정에서 본인의 실제 IP를 안전하게 숨길 수 있다.
- 인트라넷에 대하여.
    - VPN등의 방법을 이용해 사설 네트워크를 구성한다.
        - 사설 IP를 통해 구성되기 때문에 외부로부터 독립적이고 안전한 환경을 제공 받을 수 있다.
    - 적법한 절차의 인증 및 접근으로만 접글할 수 있으며, 해당 인트라넷 안에서만 리소스의 공유가 일어난다.
    - 보안 및 감사와 같은 기능 등도 사설 IP 내부에서만 공유가 일어난다.
        - 외부로의 반출 (USB 등을 통한 기기 외 반출)을 막기위해 방화벽, 암호화, 접근 제어 등의 보안 조치를 적용하곤 한다.

<aside>
❓ 질문

</aside>

- 김종혁
- 김현영
- 김현진
- 최예린
    - 선생님 일찍 잘 거 같더만 늦게 자는구만? 안 피곤?
- 하진우

### IP  차이점에 대해서

### 백엔드 서버 올렸을 때 가장 기본적인 IP = 사설 IP의 사설 IP ⇒ 172.0.0.1