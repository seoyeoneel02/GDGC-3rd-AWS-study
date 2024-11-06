# 5주차 - CloudWatch

### 4주차 과제

📌 CloudWatch 개념 정리 + 실습 과정 캡쳐본 첨부

→ 개인페이지에 링크(깃허브, 노션, 블로그) 형식으로 과제 제출

---

📌 Todo-List

- [x]  **섹션 6. AWS - CloudWatch**
<br>

## 개념

### **섹션 6. AWS - CloudWatch**

[6-1] CloudWatch란?

- AWS 리소스 사용의 실시간 모니터링 기능 지원
- 다양한 이벤트들을 수집하여 로그파일로 저장
- 이벤트&알람 설정을 통해 SNS, AWS Lambda로 전송 가능
- [CloudWatch 사용 가능 서비스들] : EC2, RDS, S3, ELB, 등
<br>

CloudWatch 모니터링 종류

1.  Basic Monitoring

    무료, 5분 간격으로 최소의 Metrics 제공
    
3. Detailed Monitoring

   유료, 1분 간격으로 자세한 Metrics 제공
<br>

CloudWatch 사용 용례

- Use Case
    - 매일 얼마나 많은 사용자들이 모바일 앱을 사용하는지 알고 싶음
    - 특정 시간대에 웹서버 상태를 점검하여 비용 절감 목표
- Potential Issue
    - 특정날에 수많은 traffic이 몰릴 수 있어 병목현상이 생길 수 있음
    - 똑같은 비용을 내며 AWS 리소스들을 사용하지만 낮시간대와 밤시간대에 필요한 서버의 성능은 달라질 수 있기 때문에 금전적 손실이 생길 수 있음 (주로 밤시간대가 낮시간대보다 서버가 오랫동안 idle)
- Solution
    - 매일 traffic rate과 특정 버튼의 유저 클릭 횟수를 분석하여 더 효율적인 앱개발을 할 수 있는 통찰력 얻을 수 있음
    - 알람 설정을 통하여 특정 threshold에 도달했을 때 개발자에게 상황을 보고해줌으로서 서버 management를 할 수 있음

<br/>

[6-2] Alarm

- 임의로 정해놓은 값에 도달할 시 Alarm을 울림
- Alarm이 울릴 시 특정 이벤트들을 작동시킬 수 있음
<br>

Alarm State

- Alarm
- Insufficient
- OK
<br>

Billing Alarm

- 우리들이 정해놓은 지출 임계값을 초과할 경우 SNS를 통하여 경고를 함
- 현재 N.Virginia(us-east-1)지역에서만 지원