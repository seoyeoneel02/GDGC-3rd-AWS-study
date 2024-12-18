# 6주차 - Lambda + CloudFront

### 5주차 과제

📌 **Lambda + CloudFront** 개념 정리 + 실습 과정 캡쳐본 첨부

→ 개인페이지에 링크(깃허브, 노션, 블로그) 형식으로 과제 제출

---

📌 Todo-List

- [x]  **섹션 7. AWS - Lambda**
- [x]  **섹션 8. AWS - CloudFront**
<br>

## 개념

### **섹션 7. AWS - Lambda**

[7-1] Lambda란?

- Serverless의 주축을 담당
    - ✨서버리스: 클라우드가 직접 서버를 돌려주고 생성하며, 리소스들을 서버의 사용량에 따라 직접 할당을 해줌 → 문제 발생 ⬇️
- Events를 통하여 Lambda를 실행시킴
    - 이벤트 ex. 업로드, 삭제
- NodeJS, Python, Java, GO등 다양한 언어 지원
    - 이벤트가 감지되었을 때 작성한 코드가 실행됨
    - 코드가 실행될 때, 마무리 될 때 다른 서비스 호출 가능
    
    → AWS 아키텍처를 구현할 때 주로 중간에 배치
- Lambda Function
: 람다에서 작성한 코드
<br>

비용

- Lambda Function이 실행될 때만 돈 지불
실행되지 않으면 비용 발생❌
- 매달 1.000.000 함수 호출 시 무료 (그 후로는 유료)

- 최대 300초(5분) 런타임 시간 허용
    - 대용량의 데이터 처리 시 타임아웃
- 512MB의 일시적인 디스크 공간 제공 (/tmp/)
    - 데이터 프리프로세싱에 사용
- 최대 50MB Deployment Package 허용
    - AWS 콘솔에서 직접 코딩
    - 로컬에서 압축파일을 업로드해서 Deployment로 배포
    - 50MB 초과 시 S3 버켓 사용
    : S3 버켓에 업로드 후 람다에서 파일에 대한 경로 지정
    유료, 1분 간격으로 자세한 Metrics 제공
<br>

사용 용례

- S3 버킷에 파일을 올리는 경우
1. put object 이벤트 발생 → 람다 함수 실행
2. 람다가 데이터를 읽고 필요하면 **데이터 변환+불필요한 데이터 삭제**
3. 변환된 데이터를 데이터베이스에 업로드

- IoT를 통하여 실시간으로 데이터가 들어오는 경우
1. 토픽(Topic)을 통해 다양한 이벤트 관리
2. 람다가 데이터를 읽고 필요하면 **데이터 변환+불필요한 데이터 삭제**
ex. 단위 유닛 변환 km - > mile
3. SNS를 통해 사용자에게 실시간으로 알림
<br>

### **섹션 8. AWS - CloudFront**

[8-1] CloudFront란?

특정 유저가 요청 시 Edge Location을 통해 웹사이트에 컨텐츠가 딜리버리 됨

<br>

- 정적, 동적, 실시간 웹사이트 컨텐츠를 유저들에게 전달
- Edge Location 사용
    - 전세계 지역마다 설치되어 있는 서버의 컬렉션 개념
    - 컨텐츠의 정보를 캐시에 보관
    - 웹사이트 접속 시 캐시에 들어있지 않다면 웹사이트 호스팅(Origin)과 소통 후 정보 저장
    - 캐시에는 컨텐츠들이 영구적으로 보관되지 않고, 특정 시간이 지나면 삭제됨
- 컨텐츠 딜리버리 네트워크 Content Delivery Network(**CDN**)
    - 컨텐츠 딜리버리 서버 웹페이지가 현재 어디에서 불려지는지,
    요청을 한 유저가 어느 지역에 있는지를 근거하여 컨텐츠 웹페이지에 딜리버리 해주는 **분산 네트워크**
    - CDN을 통해 html이나 JS 이미지 파일들을 담고 있는 컨텐츠를 가져오는 속도를 향상시킬 수 있음
- 분산 네트워크 (Distributed Network)
    - 웹사이트 호스팅 지역에서 멀어질수록 레이턴시(latency)가 커짐
    - 엣지 로케이션을 통해 유저들에게 컨텐츠 전송
<br>

- Edge Location (엣지 지역)
    - 컨텐츠들이 캐시(Cache)에 보관되어지는 장소
    - 캐시의 컨텐츠들을 유저에게 딜리버리하는 기능을 하는 서버
- Origin (오리진)
    - 원래 컨텐츠들이 들어있고, 웹서버 호스팅이 되어지는 곳
    - html 이미지 파일 드잉 존재하는 물리적 지역
    - S3, EC2 인스턴스가 오리진이 될 수 있음
- Distribution(분산)
    - CDN에서 사용되어지며 Edge Location들을 묶고 있다는 개념
<br>

## 실습

### **섹션 7. AWS - Lambda**

[7-2] Lambda 실습 - 1부

AWS Lambda - 대시보드

전체 계정 동시성(concurrency): 같은 요청이 들어왔을 때 돌릴 수 있는 함수

→ 설정해놓은 동시성 수보다 더 많은 함수 호출이 발생하면 정상적으로 작동❌

<br>

함수 생성

블루프린트 사용: AWS에서 자주 사용되는 기능들을 템플릿화

컨테이너 이미지: Doker 컨테이너처럼 AWS에서 운영되는 가상 컨테이너