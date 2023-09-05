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
    - 노드는 data 필드와 link 필드로 구성
      
      ![노드 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/Node.png)
  
        - data 필드: 원소 값을 저장, 원소의 형태에 따라 하나 이상의 필드로 구성
        - link 필드: 다음 노드의 주소 저장, 마지막 노드는 null을 저장
  - 여러 개의 작은 공간을 연결하여 전체의 자료구조를 형성
  - 자료의 논리적인 순서와 물리적인 순서가 불일치

    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/LinkedList2.png" width="300" height="200">
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/LinkedList1.png" width="300" height="200">

  - 접근, 탐색의 시간 복잡도: O(n)
    - 인덱스 i의 노드의 접근할 시 Head에서 i번 이동 / 탐색 시 Array와 동일하게 첫 노드부터 선형 탐색을 진행 
  - 삽입, 삭제의 시간 복잡도: O(1)
    - 삽입, 삭제할 노드의 주변 노드의 Link만 수정
- LinkedList의 종류
  - 연결 방식에 따라 구분
  - 단순 연결 리스트 (singly linked list)
  ![단순 연결 리스트 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/SLinkedList.png)
    - 노드에 링크 필드가 하나이며, 링크 필드를 통해 다음 노드와 연결되는 구조
    - 첫번째 노드를 모를 시 접근이 불가능하며, 첫 노드를 알면 모든 노드에 접근 가능
  - 원형 연결 리스트 (circular linked list)
  ![원형 연결 리스트 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/CLinkedList.png)
    - 단순 연결 리스트에서 마지막 노드가 리스트의 첫번째 노드와 연결되어 리스트를 원형으로 구성
  - 이중 연결 리스트 (doubly linked list)
    
  - 원형 이중 연결 리스트 (circular doubly linked list)

