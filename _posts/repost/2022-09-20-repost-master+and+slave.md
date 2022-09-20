---
title: "Master/Slave 이해하기 (MySQL Replication)"
excerpt: "Repost. 업무를 위한 지식 확장하기. 간단 ver"

categories:
  - Repost
# tags:
#   - [tag1, tag2]

permalink: /repost/about+master+and+slave/

toc: true
toc_sticky: true

date: 2022-09-20
last_modified_at: 2022-09-20
---

> 기존에 나와있는 글을 바탕으로, 스스로 공부하기 위해 재정리한 포스팅입니다.
 

### 🧩 <b>Master와 Slave의 역할</b>
- Master는 등록/수정/삭제 쿼리 요청이 오면, Binarylog를 생성하여 Slave로 전달함
- Slave는 Master의 정보를 복제해놓는 역할 담당 + 읽기 쿼리 요청 담당 (Select)
- 쿼리 요청을 분담함으로써 <u>DB 부하를 분산시키는 효과</u>가 있음 (주된 목적!)

> [Binary Log](https://myinfrabox.tistory.com/20)란?
- MySQL 서버에서 Create, Drop, Alter 같은 DDL과 Insert, Update, Delete 같은 DML을 통해 DB, 오브젝트, 데이터에 생성/수정/업데이트를 했을 때, 변화된 이벤트를 기록하는 이진 파일
- 주로 <u>복제 구성 및 특정 시점 복구</u>에 사용된다.
- (특징 및 사용법은 타이틀 링크 참고)

---

### 🧩 <b>Replication 과정</b>
<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FBtWEG%2FbtqTDcM2qJZ%2FrenWnC1FkFWOTt1y46qygk%2Fimg.jpg" width="80%">

<br>
(1) Client가 쓰기 쿼리 작업 요청, 쓰기 쿼리 요청은 Master DB가 받음<br>
(2) Master는 변경사항을 Binary Log 파일에 기록, 이후 DB에 반영(commit)<br>
(3) Slave는 현재까지 기록한 이벤트 정보 (GTID=2)를 가지고, 다음 이벤트 정보를 Master에게 요청<br>
(4) Master는 Binary Log 파일에서 최신 이벤트 정보(GTID=3)을 읽어<br>
(5) Slave에 전송<br>
(6) Slave는 Master에게 받은 이벤트 정보(GTID=3)를 Relay Log 파일에 기록<br>
(7) Slave는 최종 변경사항을 DB에 반영(commit)함<br>
<br>

> [GTID](https://hoing.io/archives/18445)란? <br>
- Global Transaction IDentifier
- MySQL 데이터베이스에서 커밋되는 각 트랜잭션과 함께 생성되고 트랜잭션에 연결되는 고유한 식별자
- 복제의 Master 서버 뿐만 아니라 복제 대상에 속한 Replica(slave) 서버에서 고유한 식별자

<br>

* (4), (5)에서는 Master 쓰레드
* (3), (6)에서는 Slave I/O 쓰레드
* (7) 과정에서는 Slave SQL 쓰레드가 동작

---

### 🧩 <b>여러 Replication 방식</b>

#### <span style="background-color:#fff5b1;"><b>Async</b></span>
- Master DB에 commit을 먼저 한 다음, replication 과정을 거침

#### <span style="background-color:#fff5b1;"><b>Semi-sync</b></span>
- Slave가 Relay Log 파일에 이벤트를 기록했는지 확인된 이후에 Master DB commit을 진행 <br>

> [Relay Log](https://blog.seulgi.kim/2015/05/how-mysql-replication.html)란?
- Slave는 I/O 쓰레드를 통해서 받은 이벤트를 로컬에 있는 file에 저장하는데, 이 파일을 relay log라고 부른다.
- 보통 relay log는 SQL thread가 이벤트를 읽고 나면 지우기 때문에 일정 정도의 크기를 넘어서지 않는다. 하지만 SQL thread가 멈추어 있으면 relay log는 계속 크기가 커지기 때문에, I/O 쓰레드는 자동으로 새 relay log 파일을 만들어서 파일이 너무 커지지 않도록 막는다.

> [I/O thread](https://blog.seulgi.kim/2015/05/how-mysql-replication.html)란?
- Slave에는 마스터에 없는 2개의 스레드가 있다. 그중 하나가 I/O thread.
- 각 Slave는 자신이 어디까지 데이터를 복사했는지 기억하고 있다.
- I/O thread는 Slave가 마지막으로 읽은 이벤트를 기억해뒀다가, Master에게 다음 이벤트를 전송해달라고 요청한다. 
- Master의 binlog dump thread가 이벤트를 보내주면 이걸 Relay log에 저장한다.
- 따라서 I/O thread가 정지되었을 때 Master의 binary log가 지워지면, Slave는 Master의 데이터를 복제할 수 없다.

<img src="https://img1.daumcdn.net/thumb/R1280x0/?scode=mtistory2&fname=https%3A%2F%2Fblog.kakaocdn.net%2Fdn%2FkxUek%2FbtqTADxldPq%2FjvSmbesX3yaRo7fPGoMYK0%2Fimg.png" width="90%"> 

---

### 🧩 <b>참고자료</b>
[MySQL Replication 이해하기 (Master - Slave)](https://it-sunny-333.tistory.com/148) <br>
