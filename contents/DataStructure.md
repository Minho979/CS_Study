# 1. DataStructure

#### Contents
- [Array](#array)
- [LinkedList](#LinkedList)
- [HashTable](#HashTable)
- [Stack](#Stack)
- [Queue](#Queue)
- [Graph](#Graph)
- [Tree](#Tree)
- [Graph와 Tree의 차이점](#Graph와-Tree의-차이점)
- [Binary Heap](#Binary-Heap)
- [Red-Black Tree](#Red-Black-Tree)
- [B+ Tree](#B+-Tree)
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
  
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/DLinkedListNode.png" width="100" height="50">
    
    - data 필드와 두 개의 link 필드로 구성
  
    ![이중 연결 리스트 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/CDLinkedList.png)

### HashTable
- HashTable의 개념
  - Key와 Value를 1:1로 연관지어 저장하는 자료구조(연관배열 구조)
  - Key를 Hash Function를 통해 Hash를 찾아 Value를 도출
    - 키 값 비교를 통한 검색이 아닌 산술적인 연산을 이용
- HashTable 기능
  - 연관배열 구조와 동일한 기능 지원
  - Key, Value가 주어질 때, 두 값을 저장
  - Key가 주어졌을 때, Key와 연결된 Value 조회
  - 기존 Key에 새로운 Value가 주어졌을 때, 기존 Value를 새로운 Value로 대체
  - Key가 주어졌을 때, 해당 Key에 연관된 Value 삭제
- HashTable 구조
  ![HashTable구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/HashTable.png)
  - Key, Hash Function, Hash, Value, 저장소(Bucket, Slot)로 구성
  - Key
    - 고유의 값
    - 저장 공간의 효율성을 위해 Hash Function에 입력하여 Hash로 변경 후 저장
      - Key는 길이가 다양하여 그대로 저장할 시 다양한 길이만큼 저장소 구성이 필요
  - Hash Function
    - Key를 Hash로 바꾸주는 역할
    - 해시 충돌(서로 다른 Key가 동일한 Hash가 되는 경우)이 발생할 확률을 최대한 줄이는 함수를 만드는 것이 중요
    - Key들을 Hash Table에 골고루 분포 시킬 수 있도록 Hash를 계산이 필요
      - 빈 공간이 있는데 충돌이 발생하는 경우 오버플로우를 유발해 좋은 Hash Function이  아님
    - 계산이 쉽고 빨라야 함
      - Key 값의 비교 연산을 수행하는 시간보다 빨라야 Hash를 사용하는 의미가 있음
  - Hash
    - Hash Function의 결과
    - 저장소에서 Value와 매칭되어 저장
  - Value
    - 저장소에 최종적으로 저장되는 값
    - 키와 매칭되어 저장, 삭제, 검색, 접근 가능
- Hash Table 동작 과정
  1. Key -> Hash Function-> Hash = Hash Function 결과
  2. Hash를 배열의 Index로 사용
  3. 해당 Index에 Value 저장, 삭제 수행
     - HashTable 크기가 10일 시 A라는 Key의 Value를 찾을 때 HashFunction("A") % 10 연산을 통해 Index 값을 계산하여 Value 조회
- Hash 충돌 (Collision)
  - 서로 다른 Key가 Hash Function에서 중복 Hash가 나오는 경우
  - 충돌이 많아질수록 탐색 시간 복잡도가 O(1)에서 O(n)으로 증가
- Hash 충돌 해결 방법
  1. Separating Chaining
     - JDK 내부에서 사용하는 충돌 처리 방식
     - Linked List(data 6개 이하) 또는 Red-Black Tree(data 8개 이상) 사용
       ![Chaining구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/HashChaining.png)
      [⬆️ h(x) = x % 5의 경우 chaining]
     - Linked List 사용 시 충돌이 발생하면 충돌 발생한 Index가 가리키고 있는 Linked List 노드 추가하여 Value 삽입
     - Key에 대한 Value 탐색 시에는 인덱스가 가리키고 있는 Linked List를 선형 검색하여 Value 반환 (삭제도 동일한 방식으로 진행)
     - Linked List 구조의 특성상 추가 데이터 수 제약이 적음
  2. Open addressing
     - 추가 메모리 공간을 사용하지 않고, HashTable 배열의 빈 공간을 사용하는 방법
     - Separating Chaining 방식에 비해 적은 메모리 사용
     - Linear Probing, Quadratic Probing, Double Hashing 방식으로 나뉨
       ![LinearProbing 방식](https://github.com/Minho979/CS_Study/blob/main/contents/images/Linearopen.png)
       [⬆️ h(x) = x % 5의 경우 Linear Probing]
       - 충돌이 발생할 시 다음 버킷을 조사하는 방식으로 검색, 저장
         - 검색의 경우 다음 버킷이 비어있거나, 마지막 버킷에 도달한 경우 검색 실패
       
  3. Resizing
     - 저장 공간이 일정 수준 채워지면 Separating Chaining의 경우 성능 향상을 위해, Open addressing의 경우 배열 크기 확장을 위해 Resizing
     - 보통 2배로 확장
     - 확장 임계점은 현재 데이터 개수가 현재 Hash Bucket개수의 75%가 될 때

- Hash Table 장점
  - 적은 리소스로 많은 데이터를 효율적으로 관리 가능
    - ex. HDD, Cloud에 있는 많은 데이터를 Hash로 매핑하여 작은 크기의 캐시 메모리로 프로세스 관리 가능
  - 배열의 인덱스를 사용하기 때문에 빠른 검색, 삽입, 삭제 가능 (O(1))
    - Hash Table의 경우 인덱스는 데이터의 고유 위치이기 떄문에 삽입 삭제 시 다른 데이터를 이동할 필요가 없어 삽입, 삭제도 빠른 속도로 수행
  - Key와 Hash에 연관성이 없어 보안 유리
  - 데이터 캐싱에 많이 사용
    - get, put 기능에 캐시 로직 추가 시 자주 hit하는 데이터 바로 검색 가능
  - 중복 제거 유용
- Hash Table 단점
  - 충돌 발생 가능성
  - 공간 복잡도 증가
  - 순서 무시
  - 해시 함수 의존도
- HashTable vs HashMap
  - Key-Value 구조 및 Key에 대한 Hash로 Value를 관리하는 것은 동일
  - Hash Table
    - 동기
    - Key-Value 값으로 null 미허용(Why? Key가 hashcode(), equals()를 사용)
    - 보조 Hash Function과 Separating Chaining을 사용하여 비교적 충돌 가능성을 낮춤 (Key의 Hash 변형)
  - Hash Map
    - 비동기 (멀티 스레드 환경에서 사용시 주의)
    - Key-Value 값으로 null 허용
- Hash Table 성능
  ||평균|최악|
  |---|---|---|
  |탐색|O(1)|O(N)|
  |삽입|O(1)|O(N)|
  |삭제|O(1)|O(N)|

### Stack
- Stack의 개념
  ![Stack의 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/Stack.png)
  - 한 끝에서만 자료를 삽입, 삭제할 수 있는 LIFO(Last In First Out) 형식의 자료 구조
- Stack의 연산
  - Stack은 LIFO를 따르기에 가장 최근에 스택에 추가한 항목이 가장 먼저 제거될 항목이다.
    - pop(): 스택에서 가장 위에 있는 항목을 제거한다.
    - push(item): item 하나를 스택의 가장 윗 부분에 추가한다.
    - peek(): 스택의 가장 위에 있는 항목을 반환한다.
    - isEmpty(): 스택이 비어 있을 떄에 true를 반환한다.
- 순차 자료구조 Stack
  ![LinearStack 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/LinearStack.png)
  - 1차원 배열을 이용하여 구현
  - 배열의 크기만큼 자료 저장 가능
  - 삽입/삭제 시 자료이동 오버헤드가 발생하지 않음
    - top에서만 삽입, 삭제가 이루어지기에 순차 자료구조임에도 자료이동 오버헤드가 존재하지 않음
  - 모든 연산 시간 복잡도는 O(1)
  - 순차 자료구조 Stack의 장점
    - 1차원 배열을 통해 쉽게 구현 가능
    - 연산의 구현이 쉽고, 빠르게 수행
  - 순차 자료구조 Stack의 단점
    - 스택 크기 변경의 비효율성
    - 빈 공간으로 메모리 낭비
- 연결 자료구조 Stack
  ![LinkedStack 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/LinkedStack.png)
  - 단순 연결 리스트를 이용하여 구현
  - 크기 변경에 자유로우며, 빈 공간으로 인한 메모리 낭비가 없음
  - 모든 연산 시간 복잡도는 O(1)
- Stack의 사용 사례
  - 재귀 알고리즘을 사용하는 경우에 유용
    - 재귀 알고리즘
      - 재귀적으로 함수를 호출해야 하는 경우에 임시 데이터를 스택에 넣어준다.
      - 재귀함수를 빠져 나와 퇴각 검색(backtrack)을 할 때는 스택에 넣어 두었던 임시 데이터를 빼 줘야한다.
      - 스택은 이러한 일련의 행위를 직관적으로 가능하게 해준다.
      - 또 스택은 재귀 알고리즘을 반복 형태(iterative)를 통해서 구현할 수 있게 해준다.
    - 시스템 스택
      - 프로그램의 호출과 복귀에 따른 순서를 관리
        - 가장 마지막에 호출된 함수가 가장 먼저 실행을 완료하고 복귀하는 LIFO 구조
        - 호출 발생 시 반환 주소 등을 스택 프레임(Stack Frame)에 저장하여 시스템 스택에 삽입
        - 실행 종료 후 시스템 스택의 top 원소(스택 프레임)을 삭제하면서 프레임에 저장된 주소로 복귀
        - 해당 과정을 반복하여 전체 프로그램이 종료되면 시스템 스택은 공백이 됨
    - 웹 브라우저 방문기록(뒤로가기)
    - 실행 취소(undo)
    - 역순 문자열 만들기
    - 수식의 괄호 검사(연산자 우선순위 표현을 위한 괄호 검사)
      - 예) 올바른 괄호 문자열(VPS, Valid Parenthesis String) 판단한기
    - 후위 표기법 계산

### Queue
- Queue의 개념
  ![Queue의 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/Queue.png)
  - 컴퓨터의 기본적인 자료구조의 한 가지로, 먼저 집어 넣은 데이터가 먼저 나오는 FIFO(First In First Out)구조로 저장
  - 순차 자료구조, 연결 자료구조 Queue의 삽입, 삭제 연산의 시간 복잡도는 O(1)  
- Queue의 연산
  - Queue는 FIFO를 따르기에 가장 처음 저장한 자료가 가장 먼저 삭제된다.
    - add(item): item을 리스트의 끝부분에 추가
    - remove(): 리스트의 첫 번쨰 항목을 제거
    - peek(): 큐에서 가장 앞에 있는 항목을 반환, 비어있는 경우 null 반환
    - isEmpty(): 큐가 비어 있을 때 true 반환
- 배열을 이용한 Queue
  - Queue의 크기 = 배열의 크기
  - 선형 Queue
    ![LinearQueue 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/LinearQueue.png)
    - 구현 간편하나 삽입, 삭제가 반복될 시 빈자리가 있지만 포화상태로 인식하는 문제 발생 가능
  - 원형 Queue

    ![CircularQueue 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/CircularQueue.png)
    - 1차 배열을 사용하되 논리적으로 처음과 끝이 연결되어 있다고 가정하고 사용
    - 선형 Queue의 포화상태 문제를 해결
- 연결리스트를 이용한 Queue

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/LinkedQueue.png" width="430" height="200">
  
  - 단순 연결리스트를 이용
    - 두 개의 포인터를 가짐
    - 크기 조절 용이
- Deque (Double-ended queue)
  ![Deque 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/Deque.png)
  - 양 끝에서 삽입, 삭제 연산이 모두 가능한 선형 자료구조
    - 양 쪽에서 연산이 이루어지므로 순차자료구조를 이용할 시 순서 변화가 많아 비효율적
  - 이중 연결리스트를 이용하여 구현
  - 삽입, 삭제 모두 O(1)의 시간 복잡도를 가짐
- Queue의 사용 사례
  - 데이터가 입력된 시간 순서대로 처리해야 할 필요가 있는 상황에 이용
    - 너비 우선 탐색(BFS, Breadth-First Search)
      - 처리해야 할 노드의 리스트를 저장하는 용도로 Queue 사용
      - 노드를 하나 처리할 떄마다 해당 노드와 인접한 노드들을 큐에 다시 저장
      - 노드를 접근한 순서대로 처리 가능
    - 캐시(Cache) 구현
    - 우선순위가 같은 작업 예약 ex) 인쇄 대기열
    - 선입선출이 필요한 대기열 ex) 티켓 카운터
    - 콜센터 고객 대기시간
    - 프린터의 출력 처리 (프린트 버퍼 큐)
    - 윈도우 시스템의 메시지 처리기
    - 프로세스 관리 (스케줄링 큐)
    - 시뮬레이션에서의 큐잉 시스템
      - 수학적 모델링에서 대기 행렬과 대기 시간 등을 모델링하기 위해 큐잉 이론(Queue Theory) 사용
      - 큐잉 이론에서 대기 행렬과 대기 시간을 실험하는데 Queue 사용

### Graph
- Graph의 개념
  - 단순히 정점(V, vertex)와 그 노드를 연결하는 간선(E, edge)를 하나로 모아 놓은 자료구조
    - 연결되어 있는 객체 간의 관계를 표현할 수 있음
    - 정점은 대상을 나타내고, 간선은 대상들 간의 관계를 나타냄
    - 그래프는 여러 개의 고립된 부분 그래프(Isolated Subgraphs)로 구성될 수 있음
    - 원소들 간의 n:n관계를 표현할 수 있음
    - 예) 지도, 지하철 노선도의 최단 경로,회로의 소자들, 도로(교차점과 일방통행길), 선수 과목 등
- Graph의 종류
  - 무방향 그래프
  - 방향 그래프
  - 완전 그래프
  - 가중 그래프
- Graph의 특징
  - 네트워크 모델
  - 2개 이상의 경로가 가능
    - 정점들 사이에 무방향/방향에서 양방향 경로를 가질 수 있음
  - self-loop뿐 아니라 loop/circuit 모두 가능
  - 루트 정점(노드)라는 개념이 없음
  - 부모-자식 관계라는 개념이 없음
  - 순회는 DFS(Depth First Search)나 BFS(Breadth First Search)로 이루어짐
  - 그래프는 순환(Cyclic) 혹은 비순환(Acyclic)
  - 그래프는 크게 방향 그래프와 무방향 그래프가 있음
  - 간선의 유무는 그래프에 따라 다름

### Tree


### Graph와 Tree의 차이점


### Binary Heap


### Red-Black Tree


### B+ Tree
