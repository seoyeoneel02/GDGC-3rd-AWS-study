# 4주차 - S3

### 3주차 과제

📌 인프런 강의 **섹션 5. AWS - S3** 수강 후 개념 정리 + 실습 과정 캡쳐본 첨부

📌 유데미 강의 **Section 12: Amazon S3 소개 + Section 13: 고급 Amazon S3 + Section 14: 아마존 S3 보안** 수강 후 개념 정리 + 실습 과정 캡쳐본 첨부

→ 개인페이지에 링크(깃허브, 노션, 블로그) 형식으로 과제 제출

---

📌 Todo-List

- [x]  **섹션 5. AWS - S3**
- [ ]  **Section 12: Amazon S3 소개**
- [ ]  **Section 13: 고급 Amazon S3**
- [ ]  **Section 14: 아마존 S3 보안**

## 개념

### **섹션 5. AWS - S3**

[5-1] S3란?

 **S3 (Simple Storage Service)** 
AWS에서 가장 처음으로 런칭한 프로그램

- **안전**하고 **가변적**인 Object 저장 공간을 제공 (ex: Google Cloud)
안전 - AWS에서 모든 파일에 일종의 안전장치를 걸어 놓아서 외부에서 접근을 불가능하게 만듦
가변적 - 저장 공간의 크기를 따로 설정하지 않아도 알아서 조절함
Object 저장 공간 - 이미지, 동영상, 파일 등만 가능. 운영체제 업로드❌
- 편리한 UI 인터페이스를 통해 어디서나 쉽게 데이터를 저장하고
불러올 수 있음
- 파일 크기는 0KB부터 5TB까지 지원
- 저장공간 무제한
→ 파티션이나 디스크 크기 할당할 필요 없이 파일 업로드 가능
- **Bucket**이라는 이름을 사용함 (디렉토리와 유사함)
- **Bucket**은 보편적인 namespace를 사용함
→ 버켓 이름은 region과 상관없이 **고유**해야 함

**S3 Object 구성요소**

- Key : 파일명
- Value : 데이터
- Version ID : S3 고유 특징
- Metadata : 데이터의 데이터. 업로드 일시, 업로드 유저 정보 등
- CORS (Cross Origin Resource Sharing)
→ 한 버켓의 파일을 다른 버켓에서 접근 가능

**S3 Data Consistency Model**

1. Read after Write Consistency (PUT)
: 파일이 S3 버켓에 업로드 되면, 즉시 사용 가능
2. Eventual Consistency (UPDATE, DELETE)
: 버켓에 업로드 된 파일 내용을 수정해도 S3 내부에서는 바로 적용되지 않음
<br/>

[5-2] S3란? - 2부

**S3 스토리지 타입**

- 일반 S3
- S3 - IA (Infrequent Access)
- S3 - One Zone IA
- Glacier
- Intelligent Tiering

**일반 S3**

- 가장 보편적으로 사용되는 스토리지 타입
- 높은 내구성 (Durability)
: 데이터의 손실 없이 잘 복원되는 정도
- 높은 가용성 (Availability)
: 데이터 접근이 용이한 정도

**S3 - IA (Infrequent Access)**

- 자주 접근 되지는 않으나 접근 시 빠른 접근이 요구되는 파일이 많을 시 유용
- 일반 S3에 비해 비용은 저렴하나 접근 시 추가 비용 발생
- 멀티 AZ를 통한 데이터 저장
→ 높은 가용성

→ 자주 접근하는 데이터를 보관하기에는 적합❌

**S3 - One Zone IA**

- 단일 AZ를 통한 데이터 저장
- 단일 AZ에 의한 데이터 접근 제한 (조금 낮은 가용성)
AZ에서 문제가 발생하여 사용이 불가능할 경우 → 해당 AZ 스토리지 사용 불가
- 데이터 접근 시 S3 - IA보다 20% 비용 저렴

**Glacier**

- 거의 접근하지 않을 데이터 저장 시 유용
- 매우 저렴한 비용
- 데이터 접근 시 대략 4-5시간 소요

**Intelligent Tiering**

- 데이터 접근 주기가 불규칙할 때 매우 유용
- 2가지 티어 존재
    - Frequent Tier
    - Infrequent Tier
- 데이터 접근 주기에 따라 두 가지 티어 중 하나로 선택됨
- Frequent Tier가 비용이 약간 더 비쌈
- 최고의 비용 절감 효율을 누릴 수 있음

**S3 요금**

- 매 GB당 돈 지불
- PUT, GET, COPY 요청 횟수당
- 데이터 다운로드 시 / 다른 리소스로 전송 시
- Metadata (object tag)
<br/>

[5-3] S3 - 버켓 생성시 알아야 할 것들

**S3 사용 용례**

파일을 임시로 혹은 영구적으로 복원할 때 사용
AWS를 사용하면서 생성되는 로그 파일들도 S3에 보관

- 파일 저장소 - 로그, 다양한 파일들(이미지, 비디오, 압축 파일 등)
S3 버켓에 특정 파일 업로드 시 이벤트를 트리거시켜서 다른 서비스를 실행시킬 수 있음
- 웹사이트 호스팅
html, css, js 등의 파일을 업로드 후 S3 버켓을 실제 도메인 DNS로 사용 가능
- CORS (Cross Origin Resource Sharing)
→ region이 다른 버켓의 데이터에 접근할 때 발생하는 에러 해결

최초 S3 버켓 생성 시 → 비공개(PRIVATE)

특정 유저 또는 그룹에게 버켓의 접근 권한을 주어야 한다면,

1. 버켓 정책 변경 (Bucket Policy)
→ 버켓의 모든 파일에 적용됨
2. 접근 제어 리스트 변경 (Access Control List)
→ 파일마다 접근 권한을 부여 가능
<br/>

[5-4] S3 암호화

**S3 암호화 (Encryption)**

AWS 내부에서 모든 것을 관리해줌 → 설정 필요 X

1. 파일 업로드/다운로드 시
    - SSL(Secure Socket Layer) - https
    - TLS(Transport Layer Security)
    SSL에서 파생해서 보안 업데이트
2. 가만히 있을 시
    1. SEE-S3 : 일정 시간마다 마스터키의 키 값 변경
    2. SSE-KMS : +누가 언제 어떻게 암호를 풀었는지를 기록
    3. SSE-C : 암호키를 직접 다룰 수 있으며, 사용자가 변경해야 함

**S3 암호화 과정**

- PUT 요청이 생성됨
    
    ```
    // HEADER
    PUT /simon-image.jpg HTTP/1.1
    Host: SimonBucket.s3.<Region>.amazonaws.com
    Date: Thu, 12 Feb 2020 14:26:00 GMT
    Authorization: authorization string
    Content-Type: text/plain
    Content-Length: 82253
    x-amz-meta-author: Simon
    Expect: 100-continue
    x-amz-server-side-encryption-parameter: AES-256
    [82253 bytes of object data]
    ```
    
    - Host : 버켓 이름. 파일이 업로드 되는 경로
    - 헤더에 x-amz-server-side-encryption-paramerer 포함
    → 파일 업로드 시 **암호화**
    - AES-256 : 암호화 알고리즘 유형