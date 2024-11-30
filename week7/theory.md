# 8주차 - VPC

### 7주차 과제

📌 **VPC** 개념 정리

→ 개인페이지에 링크(깃허브, 노션, 블로그) 형식으로 과제 제출

---

📌 Todo-List

- [x]  **VPC**
<br>

## 개념

### 관련 사전 지식

<aside>
💡

라우팅, LAN, 서브넷팅의 개념, CIDR 표기법

</aside>

### 라우팅

: 패킷에 포함된 주소 등의 상세 정보를 이용하여, 데이터 또는 메세지를 목적지까지 체계적으로 다른 네트워크에 전달하는 경로 선택(Path Determination) 그리고 스위칭 (Switching)하는 과정

여러 네트워크들의 연결을 담당하고 있는 라우터 장비가 데이터의 목적지가 어디인지 확인하여 빠르고 정확한 길을 찾아 전달한다.

<br>

**라우팅 테이블**

: 목적지까지 갈 수 있는 모든 가능성 있는 경로들 중에서 가장 효율적이라고 판단되는 경로 정보는 패킷을 전달할 때 바로 참고해서 사용할 수 있도록 따로 모아두는 공간

<br>

**패킷**

: 데이터를 전송하는 하나의 단위. 한 네트워크 회선에서 데이터 한 묶음의 단위
TCP, UDP 인지에 따라 IPv4, IPv6에 인지에 따라 형태가 달라진다.

<br>

**IP(Internet Protocol)**

: Network Layer에서 작용을 하며 인터넷 상에서 유일하게 상대를 식별할 수 있는 수단
클라이언트는 요청을 보낼 때 패킷에 IP 주소를 담고 Access Network를 통해 Network core로 보낸다.

<br>

https://annajin.tistory.com/71

<br>

### 서브넷팅

- 서브넷(subnet)
: IP 주소에서 네트워크 영역을 부분적으로 나눈 부분 네트워크
클래스를 나누어 IP를 할당하는 IPv4 주소 체계로 인해 호스트가 낭비될 수 있는 비효율성을 해결하기 위함 -> 네트워크 장치들의 수에 따라 효율적으로 사용 가능
- 서브넷 마스크(subnet mask)
: IP 주소 체계의 Network ID와 Host ID를 분리하는 역할
(서브넷 만들 때 사용!)

<img width="50%" alt="7주차 1" src="https://github.com/user-attachments/assets/760d6c45-4591-4372-b5f9-71dd08ac9d2e">

- 기본 서브넷 마스크(Default Subnet mask)
    
    A Class : 255.0.0.0
    B Class : 255.255.0.0
    C Class : 255.255.255.0
    
- 서브넷 마스크 이용
    
     IP 주소에 서브넷 마스크를 **AND** 연산 —> **Network ID**
    
    <img width="50%" alt="7주차 2" src="https://github.com/user-attachments/assets/0f15af09-5d28-4f65-8457-c920c5fc5ed9">
    
    > IP 주소 / **숫자** : 서브넷 마스크의 bit 수(왼쪽에서부터 1의 개수)
    > 
    
    ex) 192.168.32.0/24 → 해당 IP의 서브넷 마스크는 1이 24개 있음
    
<br>

**서브넷팅**

<aside>
💡 **서브넷 마스크**를 이용하여 원본 네트워크를 여러 개의 네트워크(**서브넷**)로 분리하는 과정

</aside>

🤔 IP클래스들은 이미 Network ID와 Host ID를 나타내는 부분이 구분되어 있는데
서브넷 마스크가 왜 필요할까?

❗서브넷팅을 통해 효율적인 네트워크를 사용하기 위해

- 서브넷팅 —> 서브넷 마스크의 bit 수 증가 : IP 주소 낭비 방지
- 서브넷 마스크의 bit 수를 1씩 증가
→ 할당할 수 있는 네트워크가 2배수로 증가⬆️, 호스트 수는 2배수로 감소⬇️

<img width="50%" alt="7주차 3" src="https://github.com/user-attachments/assets/c4ef69cc-ffa8-4567-a49e-aefdde98b052">

❓ -2를 하는 이유

❗ 첫번째 주소 : Network Address, 마지막 주소 : Broadcast로 쓰여서 호스트에 할당 불가

<br>

https://code-lab1.tistory.com/34

<br>

### CIDR 표기법

Classless Inter-Domain Routing : 클래스가 없는 도메인 간 라우팅 기법

- 도메인 간의 라우팅에 사용되는 인터넷 주소를 원래 IP주소 클래스 체계를 쓰는 것보다 더욱 능동적으로 할 수 있도록 할당하여 지정하는 방식
- 네트워크 정보를 여러 개로 나누어진 Sub-Network들을 모두 나타낼 수 있는 하나의 Network로 통합해서 보여주는 방법

서브넷팅 **⊂** CIDR

e.g., IP 주소 = 192.168.10.70 일 때, IP 할당 범위
192.168.10.64 ~ 192.168.10.127 → 192.168.10.70**/26**

CIDR 블럭 ≒ 서브넷

<br>

https://aws.amazon.com/what-is/cidr/

https://inpa.tistory.com/entry/WEB-%F0%9F%8C%90-CIDR-%EC%9D%B4-%EB%AC%B4%EC%96%BC-%EB%A7%90%ED%95%98%EB%8A%94%EA%B1%B0%EC%95%BC-%E2%87%9B-%EA%B0%9C%EB%85%90-%EC%A0%95%EB%A6%AC-%EA%B3%84%EC%82%B0%EB%B2%95

---

### VPC

> AWS 공식 사이트
> 
> 
> <aside>
> 💡
> 
> Amazon Virtual Private Cloud(VPC)는 사용자가 정의한 논리적으로 격리된 가상 네트워크에서 AWS 리소스를 시작할 수 있도록 하는 서비스입니다. **IP 주소** 범위 선택, **서브넷** 생성, **라우팅 테이블** 및 **네트워크 게이트웨이** 구성 등 가상 네트워킹 환경을 완벽하게 제어할 수 있습니다. 리소스 및 애플리케이션에 대한 안전하고 쉬운 액세스를 보장하도록 지원하기 위해 **IPv4** 및 **IPv6**를 VPC 내 대부분의 리소스에 대해 사용할 수 있습니다.
> 
> AWS의 기본 서비스인 Amazon VPC는 사용자 VPC 네트워크 구성을 쉽게 사용자 지정하도록 지원합니다. 인터넷에 액세스할 수 있는 웹 서버를 위해 퍼블릭 서브넷을 생성할 수 있습니다. 또한 인터넷 액세스가 없는 프라이빗 서브넷에 데이터베이스나 애플리케이션 서버 같은 백엔드 시스템을 배치하도록 지원합니다. Amazon VPC를 사용하면 보안 그룹 및 네트워크 액세스 제어 목록을 포함한 다중 보안 계층을 사용하여 각 서브넷에서 Amazon Elastic Compute Cloud(Amazon EC2) 인스턴스에 대한 액세스를 제어하도록 지원할 수 있습니다.
> 
> </aside>
> 

<img width="50%" alt="7주차 4" src="https://github.com/user-attachments/assets/15a245ab-4402-477f-a295-7c3b76b7247e">

<br>

https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/what-is-amazon-vpc.html

https://aws.amazon.com/ko/vpc/

<br>

**Virtual Private Cloud**

aws 계정 사용자 전용 **가상의 네트워크**

**Region**에 상응하는 규모의 네트워크 → 독립된 하나의 네트워크를 구성하기 위한 가장 큰 단위

- 리전에 하나씩 존재, 다른 리전과 걸쳐서 확장 불가능
- 각 리전에 종속되며 RFC1918이라는 사설 IP 대역에 맞추어 설계
- 한 번 설정된 IP 대역은 수정 불가능
- 각각의 VPC는 독립적이기 때문에 서로 통신 불가능
- VPC 및 서브넷에 대한 IPv4 지원은 VPC 및 EC2의 기본 IP 주소 지정 시스템이므로 비활성화 불가능
- VPC는 듀얼 스택 모드로 작동할 수 있음
→ 리소스는 IPv4나 IPv6 또는 둘 다를 통해 통신 가능 (IPv4 및 IPv6 통신 프로토콜은 상호 독립적)

<br>

https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-migrate-ipv6.html

<br>

**사설 IP 주소**

<aside>
💡 어떤 네트워크 안에서만 **내부적으로 사용되는 고유한 주소**

</aside>

- IP
    - 고정 IP : 컴퓨터에 고정적으로 부여된 IP
    - 유동 IP : 일정한 주기마다 사용하고 있지 않은 IP주소를 임시로 발급
    - 공인 IP : ICANN-KISA-ISP(통신업체) —> 통신사에 가입하여 발급받은 IP
        - 전 세계에서 유일
    - 사설 IP : 공유기(공인 IP)에 연결되어 있는 각 네트워크 기기에 할당
        - 하나의 네트워크 안에서 유일
        - 내부(같은 대역의 사설 IP를 할당 받은 기기)에서만 해당 IP에 접속 가능
- 사설망(Private Network)
    
    공유기를 사용한 인터넷 접속 환경일 경우 공유기까지는 공인 IP 할당을 하지만, 공유기에 연결되어 있는 가정이나 회사의 각 네트워크 기기에는 사설 IP를 할당하여 그룹으로 묶는 방법
    
    —> 아이피 번호를 중복 해서 사용 가능. IP 절약!
    

<aside>
💡

VPC는 사용 시 VPC 자체에서도 서브넷을 나눠서 사용한다.

아이피 주소를 VPC에 할당한 상황에서,
VPC를 다시 서브넷으로 나눠서 각각 서브넷을 원하는 가용영역에 배치하여 사용한다.

</aside>

VPC의 서브넷 아이피 대역에서는 총 5개의 아이피 주소를 호스트에 할당 할 수 없다.

> 서브넷의 IPv4 주소 범위에 속한 주 프라이빗 IP 주소는 인스턴스의 주 네트워크 인터페이스(eth0)에 할당된다. 각 인스턴스에는 인스턴스의 프라이빗 IP 주소를 확인하는 프라이빗(내부) DNS 호스트 이름이 할당된다.
> 
> <br>
> https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/vpc-ip-addressing.html
> 

AWS의 관리 IP로서 사용자가 사용할 수 없는 AWS의 예약 주소 (10.0.0.0/24 기준)

| 10.0.0.0 | 네트워크 주소(Network ID) |
| --- | --- |
| 10.0.0.1 | VPC 라우터(Default Gateway) |
| 10.0.0.2 | DNS 서버 주소 |
| 10.0.0.3 | AWS에서 앞으로 사용하려고 예약 |
| 10.0.0.255 | 네트워크 브로드캐스트 주소 |

→ VPC 내부적으로 **라우터**가 있고, **VPC 내부 서브넷끼리 통신**이 가능하다.

<br>

https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/configure-subnets.html

<br>

### VPC 외부 통신

**Public subnet**

인터넷에 접근 가능한 Subnet (VPC 외부/내부와 통신)

<br>

**Private subnet**

인터넷에 접근 불가능한 subnet (VPC 내부에서만 통신)

<br>

**인터넷 게이트웨이(Internet Gateway)**

서브넷이 외부와 통신 할 때, Internet Gateway를 거치게 하면 외부와 통신이 가능하게 된다.

퍼블릭 서브넷으로 만들고 싶은 서브넷을 인터넷 게이트웨이를 통해 밖으로 나가도록
**라우팅 테이블** 설정을 해야 한다.

<img width="50%" alt="7주차 5" src="https://github.com/user-attachments/assets/cd4b355f-7d8f-47c2-b47a-7fe893d69cf2">

<img width="50%" alt="7주차 6" src="https://github.com/user-attachments/assets/05f57f1e-fc99-4d6e-966f-92eed7de4bf2">

<br>

https://inpa.tistory.com/entry/AWS-%F0%9F%93%9A-VPC-%EC%82%AC%EC%9A%A9-%EC%84%9C%EB%B8%8C%EB%84%B7-%EC%9D%B8%ED%84%B0%EB%84%B7-%EA%B2%8C%EC%9D%B4%ED%8A%B8%EC%9B%A8%EC%9D%B4-NAT-%EB%B3%B4%EC%95%88%EA%B7%B8%EB%A3%B9-NACL-Bastion-Host#

https://docs.aws.amazon.com/ko_kr/vpc/latest/userguide/VPC_Internet_Gateway.html