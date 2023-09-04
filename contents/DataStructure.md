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
- Array의 시간복잡도
  - 인덱스를 알고 있으면 인덱스 접근 시간복잡도는 O(1)
  - 데이터 삽입시 기존 데이터를 한 칸씩 shift 한 후 데이터를 삽입하기에 O(n)
  - 데이터 삭제시 해당 데이터 삭제 후 데이터를 한 칸씩 shift하기에 O(n)

