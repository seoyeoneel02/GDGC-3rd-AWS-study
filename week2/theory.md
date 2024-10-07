# 3주차 - RDS

### 2주차 과제

📌 ~~인프런 강의 **섹션 4. AWS - RDS** 수강 후 개념 정리 + 실습 과정 캡쳐본 첨부~~

📌 유데미 강의 **Section 9: AWS 기초: RDS+Aurora+ElastiCache** 수강 후 개념 정리 + 실습 과정 캡쳐본 첨부

→ 개인페이지에 링크(깃허브, 노션, 블로그) 형식으로 과제 제출

---

📌 Todo-List

- [ ]  **~~섹션 4. AWS - RDS~~**
- [x]  **AWS 기초: RDS+Aurora+ElastiCache**

### Section 9: **AWS 기초: RDS+Aurora+ElastiCache**

87. Amazon RDS 개요

**RDS**

관계형 데이터베이스 서비스(Relational Database Service)의 약자
SQL을 쿼리 언어로 사용하는 데이터베이스에 대한 관리형 데이터베이스 서비스

SQL은 데이터베이스를 쿼리하는 구조화된 언어
→ 클라우드에서 RDS 서비스인 데이터베이스를 만들 수 있음

AWS의 데이터베이스 유형

- PostgreSQL
- MySQL
- MariaDB
- Oracle
- Microsoft SQL Server
- Aurora: AWS의 독점 데이터베이스

❓EC2 인스턴스 위에 자체 데이터베이스를 구축하지 않고, RDS를 사용하는 이유는?

→ RDS는 관리형 서비스: 단순 데이터베이스 제공X

- Automated provisioning, OS patching
- Continuous backups and restore to specific timestamp
- Monitoring dashboards
- Read replicas for improved read performance
- Multi AZ setup for Disaster Recovery
- Maintenance windows for upgrades
- Scaling capability
- Storage backed by EBS

❗SSH 적용은 불가능

<br/>

88. RDS 읽기 전용 복제본과 다중 AZ

**RDS Read Replicas** for read scalability

: 읽기를 스케일링함

읽지 전용 복제본을 최대 15개까지 생성 가능
→ 동일한 가용 영역 또는 리전을 걸쳐서 생성

비동기식(ASYNC) 복제

- 주된 RDS 데이터베이스 인스턴스와 두 개의 읽기 전용 복제본 사이에서 비동기식 복제 발생
- 데이터베이스로 승격시켜서 이용하는 것도 가능
: 권한을 얻어서 복제본 중 하나를 데이터베이스로 사용
- SELECT 명령문에만 사용
INSERT, UPDATE, DELETE 등 데이터베이스 수정 키워드 사용 불가

**RDS 다중 AZ**

- 동기식(SYNC) 복제
- 하나의 DNS 이름 → 스탠바이 데이터베이스에 자동으로 장애 조치
- → 가용성을 높일 수 있음

단일 AZ에서 다중 AZ로 데이터베이스 전환 가능

<br/>

90. RDS Custom for Oracle과 Microsoft SQL Server

RDS Custom
→ 기저 운영 체제나 사용자 지정 기능에 액세스 가능
→ 내부 설정 구성, 패치 적용 그리고 네이티브 기능 활성화
→ SSH 또는 SSM을 사용해서 EC2 인스턴스에 접근 가능

Oracle과 Microsoft SQL Server에서만 사용 가능
관리자 권한 전체를 가짐

↔ RDS
데이터베이스 전체를 관리

<br/>

91. Amazon Aurora 개요

AWS 고유 기술

Postgres, MySQL과 호환 가능

- 클라우드에 최적화됨
- Postgres, MySQL보다 몇 배 높은 성능
- 스토리지 자동 확장 → 저장 디스크 신경 쓸 필요 없음
- 읽기 전용 복제본 15개 생성 가능
- 즉각적인 장애 조치
- 읽기 가용성이 높음
3 AZ에 걸쳐 6개의 복제본 저장
쓰기: 4개만 있어도 가능, 읽기: 3개만 있어도 가능
- 자가 복구 과정
: 일부 데이터가 손상되거나 문제가 있으면 백엔드에서 P2P 복제를 통한 자가 복구 진행
- 단일 볼륨에 의존하지 않고 수 백 개의 볼륨을 사용
- 라이터(Writer) 엔드포인트 제공
: DNS 이름으로 항상 마스터를 가리킴
- 리더(Reader) 엔드포인트 제공
연결 로드 밸런싱에 도움 → 모든 읽기 전용 복제본과 자동으로 연결됨

<br/>

93. Amazon Aurora - 고급개념

**Auto Scaling**

복제본 오토 스케일링 → Aurora 복제본을 추가
→ 리더 엔드포인트는 새로운 replicas로 확장
→ 새로운 replicas가 트래픽을 받기 시작
→ 읽기가 더 분배되며 전체적인 CPU 사용량 낮춤

**지정 엔드포인트**

크기가 다른 상태의 2개의 복제본 존재
→ Aurora 인스턴스의 부분집합을 사용자 지정 엔드포인트로 정의

→ 사용자 지정 엔드 포인트 정의 (이후에 리더 엔드포인트 자체는 사용 X, 존재 O)

→ 업무마다 다양한 사용자 지정 엔드포인트 생성

**서버리스**

자동화된 데이터베이스 예시화와 실제 사용량에 따른 Auto Scaling 제공
→ capacity planning 필요 X

**글로벌 Aurora**

- 모든 읽기와 쓰기가 일어나는 하나의 기본 리전이 있고 최대 5개의 보조 읽기 전용 리전을 만들 수 있음 (응답 지연 1초 이하)
- 보조 리전 당 최대 16개의 읽기 전용 복제본을 사용 가능
- 한 리전에 데이터베이스 중단이 일어날 경우 재해 복구를 위해 다른 리전을 진급시킴

**Aurora Machine Learning**

AWS의 머신 러닝 서비스와 통합
: SQL 인터페이스를 통해 응용프로그램에 기계 학습 기반의 예측 추가 가능

ex. SageMaker, Amazon Comprehend

<br/>

94. RDS & Aurora - 백업과 모니터링

**RDS 백업**

- RDS 서비스가 자동으로 매일 데이터베이스의 전체 백업을 수행
5분마다 트랜잭션 로그 백업
- 수동 데이터베이스 스냅샷
: 사용자가 수동으로 트리거
수동으로 한 백업을 원하는 기간 동안 유지

**Aurora 백업**

- 자동화된 백업(1~35일), 비활성화 불가능
시점 복구 기능: 해당 기간의 어느 시점으로든 복구 가능
- 수동 DB 스냅샷

**복원**

자동화된 백업이나 수동 스냅샷을 복원할 때마다 새 데이터베이스가 생성
S3에서 MySQL 데이터베이스를 복원 가능

RDS에는 Amazon S3에서 백업 파일을 복원하는 옵션

<br/>

95. RDS Security

RDS 및 Aurora 데이터베이스에 저장된 데이터를 암호화 가능
→ 데이터가 볼륨에 암호화됨

KMS를 사용해 마스터와 모든 복제본의 암호화 진행
데이터베이스를 처음 실행할 때 정의됨

* 마스터 즉 주 데이터베이스를 암호화하지 않았다면 읽기 전용 복제본을 암호화할 수 없음

→ 암호화 되어있지 않은 기존 데이터베이스를 암호화

암호화 되지 않은 데이터베이스의 데이터베이스 스냅샷을 이용해서
암호화된 데이터베이스 형태로 데이터베이스 스냅샷을 복원

저장 데이터 암호화

클라이언트는 AWS 웹사이트에서 제공하는 AWS의 TLS 루트 인증서를 사용

<br/>

96. RDS Proxy

VPC 내에 RDS 데이터베이스를 배포할 수 있음
RDS 데이터베이스에 바로 액세스하면 완전 관리형 RDS 데이터베이스 프록시 배포 가능

Amazon RDS 프록시를 사용하면 애플리케이션이 데이터베이스 내에서 데이터베이스 연결 풀을 형성하고 공유 가능

❓RDS 데이터베이스 인스턴스에 연결이 많은 경우
데이터베이스 리소스의 부담을 줄여 데이터베이스 효율성을 향상
데이터베이스에 개방된 연결과 시간 초과를 최소화

- 완전한 서버리스
- 오토 스케일링 가능
→ 용량 관리 필요X 가용성 높음
- 다중 AZ 지원
- 데이터베이스에 IAM 인증을 강제함으로써 IAM 인증을 통해서만 RDS 데이터베이스 인스턴스에 연결하도록 설정 가능

<br/>

97. ElastiCache 개요 강의

**ElastiCache**
캐싱 기술인 Redis 또는 Memcached를 관리할 수 있도록 도와줌

캐시?
매우 높은 성능과 짧은 지연 시간을 가진 인메모리 데이터베이스
읽기 집약적인 워크로드에서 데이터베이스의 로드를 줄여줌

- 일반적인 쿼리는 캐시에 저장되므로, 매번 데이터베이스를 쿼리하지 않아도 됨
- 캐시만 사용하여 쿼리의 결과 검색 가능