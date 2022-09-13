---
title: "Preconditions and Postconditions"
excerpt: "Data Structure. 1주차 수업 기록"

categories:
  - Article
# tags:
#   - [tag1, tag2]

permalink: /data+structure/preconditions+postconditions/

toc: true
toc_sticky: true

date: 2022-09-13
last_modified_at: 2022-09-13
---
 
 ### 🧩 <b>Phases of Software Development (소프트웨어 개발 과정)</b>
Program = Data Structures + Algorithm <br>
>Data Structure : Organized collections of data <br>
>Algorithm : A set of instructions for solving a problem <br>

* Specification of the task <br>
해결해야 하는 문제에 대해 정확히 인지하는 것
* Design of a solution <br>
솔루션 설계하기, pseuducode (추상화된 코드)
* Implementation(coding) of the solution <br>
솔루션 구현하기
* Analysis of the solution <br>
개발된 프로그램에 대한 분석
* Testing and Debugging <br>
* Maintenance and the evolution of the system <br>
유지보수하기
* Obsolescence <br>
폐기처분

---

### 🧩 <b>Precontidions and Postconditions</b>
* Preconditions <br>
함수가 호출되기 전에 만족되어야 할 조건 (입력)<br>

* Postconditions <br>
함수가 호출된 후에 만족되어야 할 조건 (출력)

* 장점 <br>
  * 함수에 대한 간결한 묘사가 가능
  * 필요한 부분만 볼 수 있게끔 할 수 있음
  * 함수를 문제 없이 새로운 방법을 재구현할 수 있음

* 함수를 작성하고 나서 assert문으로 잘 동작하는지 확인할 것 (c++ 기준)
---