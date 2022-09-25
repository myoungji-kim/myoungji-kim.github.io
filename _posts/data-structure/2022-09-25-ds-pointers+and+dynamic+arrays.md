---
title: "Pointers and Dynamic Arrays"
excerpt: "Data Structure. Chapter 04."

categories:
  - data-structure
# tags:
#   - [tag1, tag2]

permalink: /data-structure/pointers+and+dynamic+arrays/

toc: true
toc_sticky: true

date: 2022-09-25
last_modified_at: 2022-09-25
---
 
### 🧩 <b>Pointer and Dynamic Memory</b>
- 포인터(pointer) : 변수의 메모리 주소 (the memory addres of a variable)
- 포인터 변수(pointer variable) : 포인터를 보관하기 위한 변수 (variable whose value is a pointer)

``` c++
Syntax:
  Type_name *var_name;
  Type_name* var_name;

Examples:
  double *ptr; // == double* ptr
  char *c1_ptr, *c2_ptr; // == char* c1_ptr, c2_ptr
```

``` c++
// Example 1
int i = 42;
int j = 80;
int *p1, *p2;
p1 = &i; p2 = &j; // 주소값 저장
p2 = p1;

cout << *p1 << endl; // 42
cout << *p2 << endl; // 42
cout << i << endl; // 42
cout << j << endl; // 80
```

``` c++
// Example 2
int i = 42;
int j = 80;
int *p1, *p2;
p1 = &i; p2 = &j; // 주소값 저장
*p2 = *p1;

cout << *p1 << endl; // 42
cout << *p2 << endl; // 42
cout << i << endl; // 42
cout << j << endl; // 42
```

#### <span style="background-color:#fff5b1;"><b>Dinamic Variable</b></span>
- <u>not declared</u>, but created during the execution of a program

#### <span style="background-color:#fff5b1;"><b>"new" operator</b></span>
- 특정한 데이터 타입의 메모리를 할당받아서 그것의 주소값을 리턴해주는 역할

#### <span style="background-color:#fff5b1;"><b>"delete" operator</b></span>
- 다이나믹 변수의 메모리를 없애줘야 한다

```c++
int *p1;
double *p2;
p1 = new int;
*p1 = 42;
p2 = new double[4];
p2[2] = 5.5;
delete p1;
delete[] p2;
```

---

### 🧩 <b>Pointers and Arrays as Parameters</b>
- Value parameters that are pointers
- Array parameters
- Const parameters that are pointers or arrays
- <u>Reference parameters that are pointers</u> (포인터를 레퍼런트 파라미터로 넘기는 경우) => 이중 포인터 사용

#### <span style="background-color:#fff5b1;"><b>Value parameters that are pointers</b></span>
``` c++
void make_it_42 (int* i_ptr) 
{
  *i_ptr = 42;
}

int *main_ptr;
main_ptr = new int;
make_it_42(main_ptr);

void make_it_all_42 (double data[], size_t n)
{
  size_t i;
  for (i=0; i<n; ++i)
    data[i] = 42;
}

double main_array[10];
make_it_all_42(main_array, 10);
cout << main_array[5];
```
