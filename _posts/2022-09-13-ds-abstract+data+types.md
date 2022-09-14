---
title: "Abstract Data Types and C++ Classes"
excerpt: "Data Structure. 2주차 수업 기록"

categories:
  - data-structure
# tags:
#   - [tag1, tag2]

permalink: /data-structure/abstract+data+types/

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
'#include "x.h"' => x.h 파일 사용 <br>

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
 
``` c++
void ThinkingCap::slots(char new_green[], char new_red[])
{
  assert(strlen(new_green) < 50); // preconditions
  assert(strlen(new_red) < 50);
  strcpy(green_string, new_green);
  strcpy(red_string, new_red); // 클래스의 멤버 함수는 클래스에서 바로 접근이 가능
}
```
* Object를 호출해야 그 안의 멤버 함수에 접근 가능함

``` c++
// green_string을 다이렉트로 사용하고 있음을 알려주고 있음
void ThinkingCap::push_green()
{
  cout << green_string << endl;
}
```

멤버 변수의 데이터를 넣기 위한 멤버 함수, <br>
멤버 변수를 사용하기 위한 멤버 함수

ThinkingCap 예제 클래스 같은 경우에는 <br>
* slot -> 데이터 삽입 <br>
* push -> 데이터 사용

---

### 🧩 <b>정리 1</b>
* Class = Data + Member Functions
* You know how to define a new class type, and place the definition in a header file.
* You know how to use the header file in a program which declares instatnces of the class type.
* You know how to activate member functions.
* But you still need to learn how to write hte bodies of a class's member functions.

---

### 🧩 <b>정리 2</b>
* Classes have member variables and member functions. An object is a variable where the data type is a class.
* You should know how to declare a new class type, how to implement its member functions, how to use the class type.
* Frequently, the member functions of a class type place information in the member variables, or use information that's already in the member variables.
* In the future we will see more features of OOP. 

---

### 🧩 <b>Classes and Parameters</b>
#### <b>Default Argument</b>
``` c++
int date_check (int year, int month=1, int day=1); // 기본값 세팅

date_check(2000); // same as date_check(2000, 1, 1);
date_check(2000, 7); // same as date_check(2000, 7, 1);
```
생성자 호출을 효율적으로 하기 위해 필요함 <br>

#### <b>Value Parameter</b>
``` c++
void swap(int a, int b)
{
  int temp = a;
  a = b;
  b = temp;
}
...
x = 1;
y = 0;
swap(x, y);
cout << x << endl; // 1
cout << y << endl; // 0
```

#### <b>Reference Parameter</b>
``` c++
// a라는 인자값을 레퍼런스로 넘긴다는 표시
void swap(int& a, int& b) 
{
  int temp = a;
  a = b;
  b = temp;
}
...
x = 1;
y = 0;
swap(x, y);
cout << x << endl; // 0
cout << y << endl; // 1
```

#### <b>Const Reference Parameter</b>
함수 호출 후, 파라미터 값 변경 불가능
``` c++
int sumOfSquare(const int& a, const int& b)
{
  return a*a + b*b;
}
...
x = 1; 
y = 0;
int i = sumOfSquare(x, y);
cout << x << endl; // 1
cout << y << endl; // 0
```

#### <b>언제 쓰나요?</b>
Case 1. The function has to modify the actual parameter.<br>
=> Reference Parameter. <br>
Case 2. It doesn't modify the actual parameter.<br>
1) If the actual parameter's data size is small.<br>
=> Value Parameter
2) If the actual parameter's data size is large. <br>
=> Const Reference Parameter (시간 단축을 위해 씀)

---

### 🧩 <b>Operator Overloading</b>
- Defining a new meaning for an operator
``` c++
bool operator == (const point& p1, const point& p2)
// postcondition: The value returned is true if p1 and p2 are identical. Otherwise, false is returned.
{
  return (p1.get_x() == p2.get_x()) &&
    (p1.get_y() == p2.get_y());
}

bool operator != (const point& p1, const point& p2)
// postcondition: The value returned is true if p1 and p2 are not identical. Otherwise, false is returned.
{
  return !(p1 == p2);
}
```
