---
title: "10가지 소프트웨어 아키텍처 패턴에 대해"
excerpt: "Article. 호기심으로 들고온 지식 한 조각"

categories:
  - Article
# tags:
#   - [tag1, tag2]

permalink: /article/10+software+architectural+patterns/

toc: true
toc_sticky: true

date: 2022-09-14
last_modified_at: 2022-09-14
---
 
### 🧩 <b>아키텍쳐 패턴이란?</b>
주어진 상황에서의 소프트웨어 아키텍쳐에서 일반적으로 발생하는 문제점들에 대한 일반화되고 재사용 가능한 솔루션 <br>
(소프트웨어 디자인 패턴과 유사하지만 더 큰 범주에 속함)

---

### 🧩 <b>10가지 소프트웨어 아키텍쳐 패턴</b>
1. 계층화 패턴 (Layered pattern)
2. 클라이언트-서버 패턴 (Client-server pattern)
3. 마스터-슬레이브 패턴 (Master-slave pattern)
4. 파이프-필터 패턴 (Pipe-filter pattern)
5. 브로커 패턴 (Broker pattern)
6. 피어 투 피어 패턴 (Peer-to-peer pattern)
7. 이벤트-버스 패턴 (Event-bus pattern)
8. MVC 패턴 (Model-view-controller pattern)
9. 블랙보드 패턴 (Blackboard pattern)
10. 인터프리터 패턴 (Interpreter pattern)

---

### 🧩 <b>1. 계층화 패턴 (Layered pattern)</b>
(= n-티어 아키텍쳐 패턴) <br>
(작성중)

---

### 🧩 <b>3. 마스터-슬레이브 (Master-slave pattern)</b>
- 마스터 컴포넌트는 동등한 구조를 지닌 슬레이브 컴포넌트들로 작업을 분산<br>
슬레이브 컴포넌트에서 처리된 결과물을 다시 돌려받아 최종 결과값을 계산하는 방식

#### <b>활용</b>
- 데이터베이스 복제에서, 마스터 DB는 <u>신뢰할 수 있는 데이터 소스</u>로 간주된다. 슬레이브 DB는 마스터 DB와 동기화된다. <br>
- 장애 허용 시스템, 병렬 컴퓨팅 시스템에 주로 활용된다.







---

### 🧩 <b>출처</b>
[[번역] 10가지 소프트웨어 아키텍처 패턴 요약](https://mingrammer.com/translation-10-common-software-architectural-patterns-in-a-nutshell/)