---
title: "클라우드란 무엇인가 (개념, 장점, 서비스 구분)"
excerpt: "Repost. 퍼블릭/프라이빗/하이브리드, Iaas/Paas/Saas"

categories:
  - Repost
# tags:
#   - [tag1, tag2]

permalink: /repost/about+cloud/

toc: true
toc_sticky: true

date: 2022-09-19
last_modified_at: 2022-09-19
---

> 기존에 나와있는 글을 바탕으로, 스스로 공부하기 위해 재정리한 포스팅입니다.
 
### 🧩 <b>클라우드 컴퓨팅이란?</b>

#### <span style="background-color:#fff5b1;"><b>개념</b></span>
- 인터넷 기반의 컴퓨팅

<img src="https://www.penews.co.kr/news/photo/202010/16772_15698_5715.png" width="60%">

- <u>인터넷 상의 가상화된 서버</u>에 프로그램을 두고, 필요할 때마다 다양한 기기에서 불러와 프로그램을 이용하는 방식
- 인터넷 연결이 되는 곳에서는 얼마든지 서버에 있는 컴퓨터 자원(CPU, 메모리, 디스크 등)을 꺼내 쓸 수 있다.

<br>

#### <span style="background-color:#fff5b1;"><b>장점</b></span>
- 서버 구매가 필요할 때 전력, 위치 확장성을 고민하지 않아도 됨
- 이미 <u>데이터 센터 안에 있는 서버를 사용하기 때문에 서버 세팅에 신경 쓸 필요 없음</u>
- 즉, 서비스 운영에만 집중할 수 있다!

<br>

- 서비스 부하가 발생할 경우, <u>실시간 확장성</u>을 지원 받을 수 있음
- 사용한 양에 비례하여 비용을 지불하기 때문에, <u>불필요한 돈이 나가지 않게 됨</u>
- 효율적인 서비스 운영 가능

---

### 🧩 <b>서비스 제공 형태</b>

#### <span style="background-color:#fff5b1;"><b>퍼블릭 클라우드(Public Cloud, 공공 클라우드, 개방형 클라우드)</b></span>
- 특정 기업이나 사용자를 위한 서비스가 아닌, <u>인터넷에 접속 가능한 모든 사용자를 위한</u> 클라우드 서비스 모델
- 클라우드 서비스 제공자가 <u>하드웨어, 소프트웨어 모두 관리</u>
- 데이터, 기능, 서버 같은 자원은 각 서비스에서 사용자별로 권한 관리가 되거나 격리되기 때문에, 서비스 사용자 간에는 전혀 간섭이 없다.

<br>

#### <span style="background-color:#fff5b1;"><b>프라이빗 클라우드(Private Cloud, 사설 클라우드, 폐쇄 클라우드)</b></span>
- 제한된 네트워크 상에서 <u>특정 기업/사용자만을 대상</u>으로 하는 클라우드 서비스
- 서비스의 자원과 데이터는 기업 내부에 저장됨
- <u>기업이 자원의 제어권</u>을 갖고 있음 => 뛰어난 <u>보안성</u>
- 개별 고객의 상황에 맞게 클라우드 기능을 <u>커스터마이징</u> 할 수 있음

<br>

#### <span style="background-color:#fff5b1;"><b>하이브리드 클라우드(Hybrid Cloud)</b></span>
- 기존 인식 : 퍼블릭 클라우드와 프라이빗 클라우드를 병행해 사용하는 클라우드
- 최근 인식 : 클라우드(가상서버)와 온프레미스(물리서버)를 결합한 형태
- 각 클라우드의 장점을 함께 취할 수 있음
  - 퍼블릭 클라우드의 <u>'유연성, 경제성, 신속성'</u>
  - 물리 서버의 <u>'보안성, 안정성'</u>
- 최근 클라우드 도입이 많아지면서, 전체 워크로드를 클라우드로 이전하기보다는 <u>주요 데이터는 물리서버에 남겨두고 트래픽을 예측하기 어려운 워크로드(ex. 이벤트, 신규 서비스 등)는 클라우드를 이용</u>하는 추세

---

### 🧩 <b>서비스 유형</b>

#### <span style="background-color:#fff5b1;"><b>IaaS (Infrasure as a Service)</b></span>
- 서비스로서의 '인프라'
- 사용자가 관리할 수 있는 범위가 가장 넓은 클라우딩 컴퓨팅 서비스
- <u>사용자가 서버 OS, 미들웨어, 런타임, 데이터와 어플리케이션까지 직접 구성하고 관리</u>할 수 있음
- 클라우드 서비스 제공업체가 데이터 센터를 구축하여 다수의 물리 서버를 가상화하여 제공하고 서버 운영에 필요한 모든 것을 책임지고 관리

> Amazon Web Service(AWS)의 EC2, Google의 Compute Engine(GCE), NHN Cloud 등

<br>

#### <span style="background-color:#fff5b1;"><b>PaaS (Platform as a Service)</b></span>
- 서비스로서의 '플랫폼'
- Iaas 형태의 <u>가상화된 클라우드 위에 사용자가 원하는 서비스를 개발할 수 있도록</u> 개발 환경(Platform)을 미리 구축해 서비스 형태도 제공
- OS, 미들웨어, 런타임 등을 미리 구축한 형태로 제공 (Iaas보다 상대적으로 낮은 자유도)
- 서비스 외적인 부분에 신경 쓸 필요 없이, 오로지 <u>애플리케이션 개발과 비즈니스에만 집중</u>할 수 있는 장점
- 인프라를 유지하고 운영하는데 별도의 인력이 소요되지 않음 => 소프트웨어 인프라 관리에 드는 비용 절약 가능

> 세일즈포스닷컴의 Heroku, Redhat의 OpenShift 등

<br>

#### <span style="background-color:#fff5b1;"><b>SaaS (Software as a Service)</b></span>
- 서비스로서의 '소프트웨어'
- 클라우드 서비스 형태 중 <u>가장 완성된 형태</u>의 클라우드 서비스
- 클라우드 인프라 위에 <u>소프트웨어를 탑재해 제공</u>하는 형태
- IT 인프라 자원, 소프트웨어 및 업데이트, 버그 개선 등의 서비스까지 모두 업체가 도맡음
- 별도의 비용으로 소프트웨어 라이센스를 구매할 필요 없음 (<u>구독 형태의 사용료</u>를 지불)
- 사용자가 자체적으로 소프트웨어를 개발하는 것 대비 초기 비용을 대폭 줄일 수 있음

> 슬랙(Slack), 마이크로소프트365(Microsoft365), 드롭박스(Dropbox) 등

---

### 🧩 <b>웹호스팅 vs 서버호스팅 vs 클라우드</b>
<img src="../assets/images/post_img/hosting_compare_01.jpeg" width="100%">

<br>

<img src="../assets/images/post_img/hosting_compare_02.jpeg" width="100%">

---

### 🧩 <b>참고자료</b>
[클라우드란 무엇인가 – 개념, 장점, 서비스 구분](https://library.gabia.com/contents/infrahosting/9114/)
