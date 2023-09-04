# 1. DataStructure

#### Contents
- Array
- LinkedList
- HashTable
- Stack
- Queue
- Graph
- Tree
- Graph와 Tree의 차이점
- Binary Heap
- Red-Black Tree
- B+ Tree
***

### Array
- Array의 개념
  - 같은 타입의 데이터를 여러개 나열한 선형 자료구조
  - 연속적인 메모리 공간에 순차적으로 데이터를 저장
  - 선언할 때 크기를 지정하면 해당 크기로 고정되며 다시 배열을 선언하기 전까지 변경 불가
  - 인덱스를 통해 배열의 요소에 접근 가능

    ![Array구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/array1.png)
- Array의 시간복잡도
  - 인덱스를 알고 있으면 인덱스 접근 시간복잡도는 O(1)
  - 데이터 삽입시 기존 데이터를 한 칸씩 shift 한 후 데이터를 삽입하기에 O(n)
  - 데이터 삭제시 해당 데이터 삭제 후 데이터를 한 칸씩 shift하기에 O(n)
 
- Array의 장점
  - 구현이 간단
  - 참조를 위한 추가적인 메모리 불필요
  - 데이터가 연속적으로 저장되어 메모리 관리 용이
  - 인덱스를 통한 접근시 검색이 빠름
- Array의 단점
  - 연산시간 문제
    - 원소의 수가 많은 경우 삽입, 삭제가 빈번하게 일어난다면 shift 오버헤드로 성능상 문제가 발생한다.
  - 배열의 크기 수정 불가능
    - 크기를 수정하기 위해서는 새로운 배열을 생성하고, 기존 데이터를 이전해야 한다.
  - 메모리 낭비가 발생
    - 선언된 배열의 사용하지 않는 공간에 메모리가 할당되어 메모리 낭비가 발생한다.

### LinkedList
- LinkedList의 개념
  - 각 노드가 데이터와 포인터를 가지고 연결되어 있는 방식으로 데이터를 저장
    - 여러 개의 작은 공간을 연결하여 전체의 자료구조를 형성
  - 자료의 논리적인 순서와 물리적인 순서가 불일치

    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/LinkedList2.png" width="300" height="200">
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/LinkedList1.png" width="300" height="200">
    
- 

