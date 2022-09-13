---
title: "Abstract Data Types and C++ Classes"
excerpt: "Data Structure. 1주차 수업 기록"

categories:
  - Data Structure
# tags:
#   - [tag1, tag2]

permalink: /data+structure/abstract+data+types/

toc: true
toc_sticky: true

date: 2022-09-13
last_modified_at: 2022-09-13
---
 
### 🧩 <b>class를 만들 때 주의할 점</b>
* Documentation <br>
클래스 상단에 클래스에 대한 설명을 적어둘 것
* Class definition <br>
(x class definition which we have already seen) <br>
클래스 껍데기에 대한 설명...
* Using the x class <br>
'#include "x.h"' => x.h 파일 사용
``` c++
#include <iostream.h>
#include <stdlib.h>
#include "x.h"

int main()
{
  X student;
  X fan;
  student.slots("Hello", "GoodBye");
}
```

---
 
### 🧩 <b>정리</b>
* Class = Data + Member Functions
* You know how to define a new class type, and place the definition in a header file.
* You know how to use the header file in a program which declares instatnces of the class type.
* You know how to activate member functions.
* But you still need to learn how to write hte bodies of a class's member functions.