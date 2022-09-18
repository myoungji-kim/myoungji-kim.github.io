---
title: "Top 10 Microservices Design Principles"
excerpt: "Article. 상위 10가지 마이크로 서비스 설계 원칙"

categories:
  - Repost
# tags:
#   - [tag1, tag2]

permalink: /repost/top+10+microservices+design+principles/

toc: true
toc_sticky: true

date: 2022-09-17
last_modified_at: 2022-09-17
---
 
### 🧩 <b>마이크로서비스 아키텍처(MSA)란?</b>

#### <b>정의</b>
- 각각을 마이크로하게 나눈 독립적인 서비스를 연결한 구조
- 소프트웨어가 잘 정의된 API를 통해 통신하는 소규모의 독립적인 서비스로 구성되어 있는 경우의 소프트웨어 개발을 위한 아키텍처 및 조직적 접근 방식
![모놀로식 vs 마이크로서비스](https://d1.awsstatic.com/Developer%20Marketing/containers/monolith_1-monolith-microservices.70b547e30e30b013051d58a93a6e35e77408a2a8.png)

<br>

#### <b>장점</b>
- 기존의 모놀로식 애플리케이션보다 더 빠르게 개발/배포/업데이트가 가능한 소프트웨어를 구축하는 방법
- 독립적 확장 가능
- 유연한 대응이 가능해 실시간으로 요구사항을 반영할 수 있음

---

### 🧩 <b>[마이크로서비스 설계 원칙 10가지](https://www.developer.com/design/microservices-design-principles/)</b>

#### <span style="background-color:#fff5b1;"><b>1. High Cohesion and Low Coupling (높은 응집력과 낮은 결합)</b></span>
- MSA는 <u>응집력이 높고 결합성이 낮아야</u> 한다.
- 즉, 각 서비스가 한 가지 작업을 잘 수행해야 한다는 뜻!
- 하나의 서비스가 매우 응집력이 있으면서도 서비스 간에 결합도가 낮아 의존하지 않도록 해야 한다.
- 낮은 수준의 결합을 통해, 많은 모듈이 서로 <u>캡슐화</u>된 상태로 있어야 응용 프로그램도 쉽게 테스트를 할 수 있다.
<br>

#### <span style="background-color:#fff5b1;"><b>2. Discrete Boundaries (개별 경계)</b></span>
- 마이크로서비스는 <u>작고 독립적으로 배포할 수 있는</u> 기능 단위 => 관리 및 확장이 더 쉬움
  - 온라인 쇼핑몰을 예로 들면, 로그인 마이크로서비스와 구매/청구 프로세스를 처리하는 마이크로서비스로 나뉠 수 있음
- MSA를 설계할 때는 서비스끼리의 기능 간 종속성을 피해야 한다.
  - ex. 인증/권한 부여 서비스와 사용자 프로필 관리 서비스
  - 만약 프로필 관리 서비스가 작동하기 위해 인증/권한 부여 서비스가 반드시 호출되어야 한다면?
  - 이런 종속성은 매우매우 좋지 않음!!!!
  > 이런 종속성을 피하고 싶다면? <br>
  => 한 서비스의 요청을 다른 서비스가 이해할 수 있는 요청으로 변환하는 [API 게이트웨이](https://cloud.google.com/api-gateway/docs/architecture-overview?hl=ko)를 구현할 것, 그런 다음 게이트웨이는 받은 요청을 상대 서비스에 대해 이해할 수 있는 호출로 변환해야 함
<br>

#### <span style="background-color:#fff5b1;"><b>3. Single Responsibility Principle (단일 책임 원칙)</b></span>
- 클래스가 언제든지 <u>변경되는 이유는 단 하나</u>여야 한다!
- 단일 책임 원칙을 준수해야 유지 관리 및 업데이트가 더 수월하며, 다른 마이크로서비스와의 충돌 가능성도 줄어든다.
- MSA 설계 시 이 원칙은 무조건 지켜야 한다.
<br>

#### <span style="background-color:#fff5b1;"><b>4. Design for Failure (실패를 위한 설계)</b></span>
- <u>한 서비스의 장애가 다른 서비스에 영향을 미치지 않아야</u> 한다.
- 예를 들어 개발자가 DB 서비스와 애플리케이션 서비스를 제공하고 있다고 하자.
  - 혹여 DB 서비스가 다운되어도, 애플리케이션 서비스는 계속 실행이 되어야 한다. 
  - 이로써 애플리케이션의 가용성을 높이고, 손상된 종속성을 수정하는데 필요한 작업량을 줄일 수 있다. 
<br>

#### <span style="background-color:#fff5b1;"><b>5. Business Capabilities (비즈니스 기능)</b></span>
- 각 서비스는 특정 비즈니스 기능을 담당해야 한다.
- 모든 서비스는 함께 애플리케이션에 필요한 모든 비즈니스 기능을 다룰 수 있어야 한다.
- 필수적인 이유 
  - 서비스를 작은 단위로 쉽게 관리할 수 있는 상황을 유지할 수 있다. 각 서비스가 하나의 비즈니스 기능만 담당한다면 필요에 따라 상황을 이해하고 변경하는게 훨씬 쉬워진다.
  - 애플리케이션 확장에 도움이 된다. 각각의 서비스를 독립적으로 확장할 수 있다면, 다른 부분에 영향을 주지 않고 특정 파트만 확장할 수 있다.
- 하나의 서비스가 중단되어도, 다른 서비스는 계속 작동하고 있기 때문에 사용자의 불편함을 줄일 수 있다.
<br>

#### <span style="background-color:#fff5b1;"><b>6. Decentralization (탈중앙화)</b></span>
- MSA는 <u>각 서비스가 자체 데이터 복사본을 유지/관리</u>한다. 
- 여러 서비스가 하나의 DB에 집중되어 있지 않기 때문에, <u>로깅 및 캐싱을 쉽게 구현</u>할 수 있다.
<br>

#### <span style="background-color:#fff5b1;"><b>7. Process Automation (프로세스 자동화)</b></span>
- 아주 중요! <u>프로세스를 자동화</u>함으로써 안정성을 개선하고, 비용을 절감하며, 소프트웨어 개발 주기를 단축시킬 수 있다.
- MSA는 모놀리식과 달리 여러 배포 단위를 관리해야 한다. 즉, MSA의 배포 프로세스를 자동화할 수 있어야 한다.
<br>

#### <span style="background-color:#fff5b1;"><b>8. Inter-Service Communication (서비스 간 통신)</b></span>
- 기존 모놀리식 애플리케이션을 마이크로서비스로 나눌 때, <u>서비스들이 통신하는 방법을 정의</u>해야 한다.
- MSA에서 서비스 간 통신을 구현하는 몇 가지 방법
  - 이벤트 기반 접근 방식 : 다른 서비스가 구독하고 반응할 수 있는 이벤트를 게시하기
  - HTTP, AMQP와 같은 프로토콜 사용 : 구현 세부 정보에 대한 지식이 없어도 서비스 간에 메시지 교환이 가능함
- 서비스가 내부적으로 작동하는 방식에 대한 기술적인 세부 사항을 캡슐화하고, API 기능을 노출하여 다른 서비스가 해당 API 메소드를 통해 서비스에 엑세스할 수 있도록 해야 함
<br>

#### <span style="background-color:#fff5b1;"><b>9. Monitoring (모니터링)</b></span>
- MSA는 '분산 특성' 때문에 수동적으로 프로세스를 구축하여 오류를 식별하기는 너무 어렵다.. 그래서 <u>자동 모니터링 시스템</u>이 필요하다.
- 함께 읽어보면 좋을 포스팅 : [MSA 와 Log - 중앙 집중식 로깅 ELK stack 편](https://bravenamme.github.io/2021/01/28/elk-stack/)
<br>

#### <span style="background-color:#fff5b1;"><b>10. Command Query Responsibility Segregation(CQRS) (명령 쿼리 책임 분리)</b></span>
- CQRS : <u>읽기 및 쓰기 작업을 별도의 클래스로 분리</u>하는 디자인 패턴
- CQRS 패턴은 일반적으로 MSA에서 사용되는데, 다른 구성 요소가 응용 프로그램 기능의 다른 부분을 담당할 수 있어 확장 및 유지 관리가 더 용이하다. 
- CQRS에 대한 데이터 접근은 단일 DB로 제한되어 있다 => 여러 서비스 DB에 걸쳐 있는 복잡한 쿼리에 유용함
- CQRS 디자인에는 command / query 두 섹션이 있음
  - command : 명령문 생성, 편집 및 삭제
  - query : 명령문 읽기
- 장점
  - 쓰기와 독립적으로 읽기를 확장할 수 있음
  - 각 클래스에 책임이 있을 때 데이터 무결성을 관리하기 더 쉬움
  - 각 클래스는 하나의 책임만 가지기 때문에, 코드를 더 테스트하기 쉽게 만들 수 있다.

---

### 🧩 <b>실제 기업들의 MSA 전환기</b>
1. [[2019] PAYCO 쇼핑 마이크로서비스 아키텍처(MSA) 전환기](https://www.youtube.com/watch?v=l195D5WT_tE)
<br>
2. [[우아콘2020] 배달의민족 마이크로서비스 여행기](https://www.youtube.com/watch?v=BnS6343GTkY)
<br>
