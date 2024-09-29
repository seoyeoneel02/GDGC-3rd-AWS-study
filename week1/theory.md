# 2주차 - EC2

### 1주차 과제

📌 개인페이지 자기소개 작성하기

📌 인프런 강의 **섹션 1. AWS - Introduction + 섹션 2. AWS - IAM** 는 각자 자유롭게 공부하기

📌 인프런 강의 **섹션 3. AWS - EC2** 수강 후 개념 정리 + 실습 과정 캡쳐본 첨부
→ 개인페이지에 링크(깃허브, 노션, 블로그) 형식으로 과제 제출

---

📌 Todo-List

- [x]  **섹션 1. AWS - Introduction**
- [x]  **섹션 2. AWS - IAM**
- [x]  **섹션 3. AWS - EC2**

<br/>

## 개념

### 섹션 1. AWS - Introduction

[1-1]

AWS?

Amazon Web Service 의 약자

클라우드 컴퓨팅 서비스
: 원격상에 존재하는 서버가 직접 작동되고 운영되며 데이터가 프로세싱 되는 것
→ 로컬 컴퓨터와 상관 없음

서버리스(Serverless) 기능 지원
: 원격(클라우드)에서 서버를 작동시키고 관리하며 메모리 활동에 대해 유연한 방식을 채택하여 혼자 생존함

<br/>

[1-2]

As You Pay Go 서비스
서비스를 사용하는 만큼 해당하는 비용을 지불

Free-tier 서비스

루트(Root) 사용자
→ 다른 유저를 만들거나 삭제 또는 권한을 부여할 수 있음

<br/>

### 섹션 2. AWS - IAM

[2-1]

IAM?

Identity and Access Management 의 약자

사용자들의 계정에 대한 관리가 목적

: 유저를 관리하고 접근 레벨 및 권한에 대한 관리를 가능하게 해줌

<br/>

루트 유저 안에서 다른 유저를 생성 가능

IAM은 생성한 유저에 대한 접근키와 비밀키를 생성해준다
→ 이 권한으로 AWS 서비스를 원격에서 사용할 수 있음

접근키(Access Key), 비밀키(Secret Access Key)

매우 세밀한 접근 권한 부여 가능 
ex. 테이블 생성 기능만 허용

비밀번호를 수시로 변경 가능하게 해줌

Multi-Factor Authentication(다중 인증) 기능

<br/>

그룹(Group): 하나 또는 다수의 유저가 존재할 수 있음

유저(User): 

역할(Role): 하나 혹은 다수의 정책을 지정할 수 있음 → 유저마다 다양한 정책을 부여함으로써 다른 권한을 위임할 수 있음

정책(Policy): JSON 형태로 되어있는 document
세밀한 접근 권한을 일일이 설정하여 하나의 정책 다큐먼트를 만들 수 있음
→ 다양한 정책을 만들어 다양한 접근레벨 및 권한이 가능해짐

<br/>

(*) 정책은 그룹, 역할에 추가시킬 수 있다.

(*) 하나의 그룹 안에 다수의 유저가 존재 가능하다.

→ 그룹의 역할 또는 정책을 추가시키게 된다면 그룹 안에 있는 모든 유저에게 영향이 감

<br/>

IAM은 유니버셜(Universal) 함
→ 지역 설정이 필요 없음

대부분의 서비스는 Regional함
: 지역마다 제공하는 리소스와 기능들이 다를 수 있음

<br/>

[2-2]

IAM 정책 시뮬레이터

개발환경(스테이징, 디벨롭) 과 실제환경 (프로덕션)
두 가지의 다른 환경에서 소프트웨어 개발이 이루어지고 유지됨

: 프로덕션으로 넘어가기 전 테스트 환경에서 미리 정의를 내린 정책 또는 역할들이 원하는대로 잘 작동하는지 확인하는 툴

1. 개발환경(Staging or Develop)에서 실제환경(Production)으로 빌드하기 전 IAM 정책이 잘 작동되는지 테스트하기 위함
2. IAM과 관련된 문제들을 디버깅하기에 최적화된 툴 (이미 실제로 유저에 부여된 다양한 정책들도 테스트 가능)

<br/>

### 섹션 3. AWS - EC2

[3-1]

EC2?

Elastic Compute Cloud
: 클라우드라는 공간에서 크기가 유연하게 변경되는 기능 제공

<br/>

EC2 사용시 내는 다양한 지불 방법

On-demand: 시간 단위로 가격이 고정되어 있음
소프트웨어 및 서버 개발 초기 단계에서 종종 쓰이기도함

Reserved: 한정된 EC2 용량 사용 가능, 1-3년 동안 시간별로 할인 적용 받을 수 있음.
저렴한 가격에 사용할 수 있음

Spot: 입찰 가격 적용. 가장 큰 할인률을 적용받으며 특히 인스턴스의 시작과 끝기간이 전혀 중요하지 않을 때 매우 유용.

<br/>

1. On-demand
:오랜 시간동안 선불을 내지 않고 최소한의 비용을 지불하여 EC2 인스턴스를 사용하고 싶을 때, 특히 앱/프로그램 개발 시 최초로 EC2 인스턴스에 deploy 할 때 매우 유용
기간을 미리 알 수 없는 경우에 유용. 단기간에 끝낼 수 있을 때 사용. 개발 초기단계에 EC2 인스턴스에 처음 테스트할 때 적합
2. Reserved
: 안정된, 예상 가능한 workload 시 Reserved 사용 권장, 선불로 인한 컴퓨팅 비용 대폭 감소
개발의 시작과 끝을 알고 있는 경우 유용. 선불로 특정한 금액을 지불할 경우 추가적으로 지정되는 컴퓨팅 시스템을 사용할 수도 있음. 요구사항이 자주 반복되지 않고 안정적으로 흘러가며 개발의 시간에 대해 예측이 가능할 때 적합.
3. Spot
: 단순히 비용 절감 시 유용함. 인스턴스의 시작/끝시점에 구애받지 않을 경우 권장
개발 시각과 끝 시각에 구애받지 않고 예측하기 어려운, 그러나 아주 저렴한 가격으로 이용하고 싶을 때 적합

EC2를 사용하기 위해 EBS라는 디스크 볼륨을 요구한다.
EBS: EC2 안에 부착되어 있는 일종의 하드 디스크. 가상디스크

<br/>

[3-2]

EBS?

Elastic Block Storage 의 약자.

- 저장 공간이 생성되어지며 EC2 인스턴스에 부착된다
- 디스크 볼륨 위에 File System이 생성된다
- EBS는 특정 Availability Zone에 생성된다

<br/>

스토리지 볼륨을 생성하여 EC2 인스턴스에 부착되어 사용됨

EBs는 디스크 볼륨 위에 파일 시스템이 생성 되어진다

→ EC2 인스턴스에 접근이 가능할 뿐만 아니라 파일을 로컬 디스크로 옮기는 작업도 가능해짐

Availability Zone: 하나의 리전안에 여러개의 az가 존재할 수 있음

az라는 백업을 통해 서비스 제공을 가능하게 해주는 일종의 diasater recovery

<br/>

ebs 볼륨 타입

- SSD군
    - General Purpose SSD(GP2): 최대 10K IOPS를 지원하며 1GB당 3IOPS 속도가 나옴.
    SSD 군에서 가장 보편적으로 사용됨.
    - Provisioned IOPS SSD(I01): 극도의 I/O률을 요구하는(매우 큰 DB 관리) 환경에서 주로 사용됨. 10K 이상의 IOPS를 지원함.
    아주 방대한 양의 데이터 처리 시 필요함. 입출력의 비중이 매우 빈번하고 그 양이 방대할 경우 뛰어난 효능을 보임
- Magnetic/HDD군 (4분 25초)
    - Throughput Optimized HDD (ST1): 빅데이터 Datawarehouse, Log 프로세싱시 주로 사용(boot volume으로 사용 가능X)
    빅테이터를 보관하며 컴퓨터 로그 팡일을 보관하고 읽을 시 추천
    하지만 부트 볼륨으로는 사용 불가능함 : 윈도우처럼 운영체제를 가지고 있을 수 없음
    - CDD HDD (SC1): 파일 서버와 같이 드문 volume 접근 시 주로 사용, 역시 boot volume으로 사용 불가능하나 비용은 매우 저렴함
    파일 서버처럼 입출력의 비율이 빈번하지 않은 경우 주로 사용
    초당 어마어마한 양의 로그 파일이 생성되는 것과 달리 SC1은 빈번한 입출력이 필요 없고 오랫동안 보관해도 괜찮은 데이터들을 처리할 때 쓰임
    부트 볼륨으로 사용 불가능함
    - Marnetic (Sandard): 디스크 1GB 당 가장 싼 비용을 자랑함. Boot volume으로 유일하게 가능함
    가장 싼 디스크 볼륨. 부트 볼륨으로 사용 가능함

<br/>

[3-3]

ELB? (Elastic Load Balancers)

- 수많은 서버의 흐름을 균형있게 흘려보내는데 중추적인 역할을 함
- 하나의 서버로 traffic이 몰리는 병목현상(bottleneck) 방지
→ 서버의 원활한 흐름 및 속도에 도움
- Traffic의 흐름을 Unhealthy instance -> healthy instance로
(Unhealthy 원인: 셧다운, 시간 초과 등)

<br/>

ELB 타입

1. Application Load Balancer
: OSI Layer7(Application Layer)에서 작동됨

→ HTTP, HTTPS와 같은 traffic의 load balancing에 가장 적합

→ 고급 request 라우팅 설정을 통하여 특정 서버로 request를 보낼 수 있음
: root를 변경시켜줌

2. Network Load Balancer
: OSI Layer4에서 작동됨, 매우 빠른 속도를 자랑하며 Production환경에서 종종 쓰임

→ 극도의 performance가 요구되는 TCP traffic에서 적합함
→ 초당 수백만개의 request를 아주 미세한 delay로 처리 가능

3. Classic Load Balancer
: 현재 Legacy로 간주됨, 따라서 거의 쓰이지 않음

→ Layer7의 HTTP/HTTPS 라우팅 기능 지원
→ Layer4의 TCP traffic 라우팅 기능도 지원

EC2를 사용할 때 ELB가 에러를 발견하여 504 에러 메시지 제공
: 어플리케이션이나 서버가 응답을 받지 못하는 경우

→ 웹서버 레이어 또는 데이터베이스 레이어에서 해결 가능

<br/>

X-Forwarded-For 헤더

ex. 152.12.3.225 (public IP address)
→ DNS 리퀘스트를 통하여 ELB에 도달
→ ELB는 리퀘스트를 받고 10.0.0.23 (Private IP address)로 인식
→ EC2 인스턴스로 리퀘스트를 전송

*EC2는 Private IP address만 볼 수 있음

→ X-Forwarded-For 헤더를 통해 원래의 public IP address를 찾아볼 수 있음

<br/>

[3-4]

Route 53

AWS에서 제공하는 DNS 서비스

- EC2 instance
- S3 Bucket
- Load Balancer

<br/>

[3-6]

PuTTY : SSH를 사용하여 원격 서버에 접속할 수 있게 해주는 오픈 소스 터미널 어플리케이션

PuTTYgen: EC2 PEM 파일을 PPK 파일로 변환