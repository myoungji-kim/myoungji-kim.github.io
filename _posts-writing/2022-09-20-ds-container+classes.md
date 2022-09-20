---
title: "Container Classes"
excerpt: "Data Structure. Chapter 03."

categories:
  - data-structure
# tags:
#   - [tag1, tag2]

permalink: /data-structure/container+classes/

toc: true
toc_sticky: true

date: 2022-09-20
last_modified_at: 2022-09-20
---
 
### 🧩 <b>Container Classes</b>
- 자료구조의 기본은 컨테이너 클래스
- 컨테이너의 클래스는 많은 아이템을 갖고 있는데, add, remove, examine 하는 것이 ㅣ기본 기능 (찾고, 넣고, 빼기)

<br>

#### ..?
(그냥 빈 가방(클래스)이 있는데 숫자(데이터)를 넣고 빼고 하는 모습을 자세하게 보여주심)

<br>

#### <span style="background-color:#fff5b1;"><b>Summary of the Bag Operation</b></span>
- A bag can be put in its <u>initial state</u>, which is an empty bag.
- Numbers can be <u>inserted</u> into the bag.
- You may check how many <u>occurrences</u> of a certainnumber are in the bag.
- Numbers can be <u>removed</u> from the bag.
- You can check <u>how many</u> numbers are in the bag.

<br>

#### <span style="background-color:#fff5b1;"><b>Default Constructor</b></span>

``` c++
bag::bag()
// Postcondition: The bag has been initailized and it is now empty.
{
  ...
}
```

<br>

#### <span style="background-color:#fff5b1;"><b>The Insert Function</b></span>

``` c++
void bag::insert(int new_entry)
// Precondition: The bag is not full.
// Postcondition: A new copy of new_entry has benn added to the bag.
{
  ...
}
```

<br>

#### <span style="background-color:#fff5b1;"><b>The Size Function</b></span>

``` c++
#inclue <cstdlib>
// size_t => unsigned int (음이 아닌 정수)
std::size_t bag::size() const
// Postcondition: The return value is the number of integers in the bag.
{
  ...
}
```

<br>

#### <span style="background-color:#fff5b1;"><b>The Occurrences Function</b></span>

``` c++
#inclue <cstdlib>
std::size_t bag::occurrences(int target) const
// Postcondition: The return value is the number of copies of target in the bag.
{
  ...
}
```

<br>

#### <span style="background-color:#fff5b1;"><b>The Remove Function</b></span>

``` c++
void bag::remove(int target)
// Postcondition: If target was in the bag, then one copy of target has been removed from the bag; otherwise the bag is unchanged.
{
  ...
}
```

<br>

#### <span style="background-color:#fff5b1;"><b>Using the Bag in a Program</b></span>

``` c++
bag ages;
// Record the ages of three children:
ages.insert(4);
ages.insert(8);
ages.insert(4);
```

<br>

#### <span style="background-color:#fff5b1;"><b>The Header File and Implementation File</b></span>

- The programmer who wirtes the new bag class must write two files:
1. bag1.h <br>
  a header file that contains documentation and the class definition
2. bag1.cxx <br>
  an implementation file that contains the implementations of the bag's member functions.

``` c++
// 1-1) bag's documentation
// 1-2) bag's class definition
// 2) Implementations of the bag's member functions
```

<br>
 
#### <b>Documentation for the Bag Class</b>
- The documentation gives <u>prototypes and specifications</u> for the bag member functions.
- Specifications are written as <u>precondition/postcondition</u> contracts.
- Everything needed to use the bag class is included in the comment.

 
#### <b>The Bag's Class Definition</b>
- 클래스 정의
 
#### <b>The Implementation File</b>
- 코드 작성 / 구현

---

### 🧩 <b>A Quiz</b>
Q. Suppose that a Mysterious Benefactor provies you wuth the Bag class, but you are only permitted to read the documentation in the header file. You cannot read the class definition or implementation file. Can you write a program that uses the bag data type?
<br><br>
A. Yes, I can. <br>
You know the name of the new data type, whice is enough for you to declare bag variables. You also know the headings and specifications of each of the operations.

--- 
### 🧩 <b>Implementation Details</b>

#### <b>예제</b>

``` c++
class Bag
{
  public:
    static const size_t CAPACITY = 20;
    ...
  private:
    int data[CAPACITY];
    size_t used;
}
```

#### <b>An Example of Calling Insert</b>
``` c++
void bag::insert(int new_entry) 
```

<br>

#### <b>Pseudocode for bag::insert</b>
* `assert(size() < CAPACITY)`
* Place `new_entry` in the appropriate location of the `data` array.
* Add one to the member variable `used`.

<br>

#### <b>C++ code for bag::inesrt</b>
``` c++
typedef int value_type;

// int 대신에 어떤 타입이라도 받기 위해 value_type으로 설정
// 크기가 너무 커지는 것을 방지하기 위해 const
void bag::insert(const value_type& entry)
{
  assert(size() < CAPACITY);
  data[used++] = entry;
}
```

<br>

#### <b>C++ code for bag::erase_one</b>
```c++
bool bag::erase_one(const value_type& target)
{
  size_type index = 0;
  while ((index < used) && (data[index] != target))
    ++index;
  if (index == used)
    return false;
  --used;
  data[index] = data[used];
  return true;
}
```

<br>

#### <b>C++ code for bag::operator +=</b>
```c++
#include <algorithm>
#include <cassert>

void bag::operator +=(const bag& addend)
{
  assert(size() +addend.size() <= CAPACITY);

  // copy(beginning location, Ending location, Destination)
  copy(addend.data, addend.data+addend.used, data+used);
  used += addend.used;
}
```

---

### 🧩 <b>Summary</b>

* A container class is a class that can hold a collection of items.
* Container classes can be implemented with a C++ class.
* The class is implemented with a header file (containing documentation and the clas definition) and an implementation file (containing the implementations of the member functions).
* Other details are given in Section 3.1 (인터넷에서 다운 가능), which you should read.
