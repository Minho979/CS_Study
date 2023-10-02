# B+ Tree
## B+Tree 개념

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/B%2BTree.jpg" width="700">
  
  - B트리를 linear하게 탐색해야하는 경우 중위 탐색을 통해 트리 전체를 탐색하게 되어 발생하는 성능 저하를 개선하기 위해 고안
  - 모든 키 값이 리프 노드에 정렬되어 있는 트리 구조
    - 오름차순으로 정렬
  - 동작 방식은 B트리와 유사하지만 리프 노드는 연결리스트의 형태를 띄어 선형 검색이 가능
    - 탐색에 시간 있어서 유리하여 데이터베이스 시스템 구조에 채택
    - 순차 집합(Sequence Set)이라고도 함
  - 오직 리프 노드에서만 레코드 포인터를 가짐
  - 모른 리프 노드는 왼쪽에서 오른쪽으로 연결
  - 리프 노드가 아닌 노드는 인덱스 노드로 부르며 리프 노드 자료는 데이터 노드라고 부름
    - 인덱스 노드: Value 값에 다음 노드를 가리키는 포인터 주소가 존재
    - 데이터 노드: Value 값에 데이터가 존재
  - 인덱스 노드와 데이터 노드의 키 값이 중복될 수 있음
    - Ex) index node key 5, data node key 5 가능
    - 인덱스 노드는 데이터의 빠른 접근을 위한 인덱스 역할만 수행하기 때문에 가능
    - 데이터 노드에서는 데이터가 중복되지 않음

## B+Tree 특징
  - 모든 Key, data는 리프 노드에 모여있음
  - 모든 리프 노드는 같은 레벨에 존재하며 연결리스트 형태를 띔
    - 재탐색시 데이터 순회 시간이 절약됨 `O(log n)`
  - 리프 노드의 부모 Key는 리프 노드의 첫번쨰 Key보다 작거나 같다
    - 리프 노드의 Key를 부모 노드가 가지고 있는 경우이기에 데이터의 삽입과 삭제 시 Key에 변형이 일어남
    - Key의 변경이 없는 경우도 존재
  - 데이터 노드의 자료는 정렬되어 있음
    - 오름차순 정렬
  - 데이터 노드에서 데이터가 중복되지 않음
  - 그외 M차 B트리와 M차 B+트리는 동일한 특징을 가짐

    1\. 노드에는 2개 이상의 데이터(Key)가 들어갈 수 있으며, 항상 정렬된 상태로 저장한다

    2\. 루트 노드와 리프 노드를 제외한 내부 노드는 M/2 ~ M개의 자식을 갖는다(최소 절반 이상은 갖는다)
       
       - 최대 M개의 자식을 가질 수 있는 B트리를 M차 B트리라고 한다
       - 루트 노드는 최소 2개의 자식을 갖는다
    
    3\. 특정 노드의 데이터(Key)가 K개라면, 자식 노드의 개수는 K+1개여야 한다

    4\. 특정 노드의 왼쪽 서브 트리는 특정 노드의 Key보다 작은 값들로, 오른쪽 서브 트리는 큰 값들로 구성된다

    5\. 노드 내에 데이터(Key)는 floor(M/2)-1개부터 최대 M-1개까지 포함될 수 있다

    6\. 최소 차수는 자식수의 하한 값을 의미하며, 최소차수가 t라면 M = 2t - 1을 만족

    7\. 모든 리프 노드들이 같은 레벨에 존재한다

### B-Tree와 B+Tree의 차이점
- 리프 노드에 모든 키와 데이터가 존재 / 정렬 / 연결리스트로 연결 `O(log n)`
- non-leaf node에는 키 값과 포인터만 존재
- 키 값의 중복 등장 가능

## B+Tree의 탐색 과정
  - 전반적인 과정은 B Tree와 동일하나 B+Tree는 모든 경우에 대해 리프 노드로 가서 순차 탐색을 통해 데이터 탐색
    - B Tree의 경우 Best Case에는 루트 노드에서 탐색 종료

## B+Tree의 삽입 과정
  - 삽입시 트리의 Key가 변경되는 경우로 설명
  - B트리와 유사하지만 리프 노드에서 최대 Key개수를 초과할 때가 다름
  1. 탐색 과정을 통해 삽입하고자 하는 노드의 위치 파악
  2. 리프 노드가 가득차지 않은 상태라면 오름차순 정렬에 맞게 삽입
  3. 리프 노드가 가득찬 상태라면 노드를 분할
     1. 새로운 리프 노드를 구성하고 기존 리프 노드 데이터의 절반을 옮김
        - 새로운 리프 노드의 최소 키(기존 리프 노드의 중간값)를 부모 노드에 삽입하여 기준 포인터로 설정
        - 부모 노드 역시 리프 노드의 Key를 받았기에 가득찬 상태인지 체크해야 함
          - 부모 노드가 쪼개지지 않는 시점이 올 떄까지 상향식으로 반복
  4. 루트가 쪼개지면 새로운 루트 노드를 생성하되 1개의 Key와 2개의 양쪽 포이너로 구성되야 하며 기존 루트 노드의 중간 Key는 새로운 루트 노드에 저장한 뒤 제거
  
### 삽입 Case

- **Case 1: 분할이 일어나지 않고, 삽입 위치가 리프 노드의 가장 앞 Key 자리가 아닌 경우**
  - B트리 삽입 Case 1과 동일한 삽입 과정 수행

- **Case 2: 분할이 일어나지 않고, 삽입 위치가 리프 노드의 가장 앞 Key 자리인 경우**
  - 삽입 후 부모 Key를 삽입된 Key로 갱신하고, data 삽입

      <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/B%2BTree-Insert2-1.jpg" width="600">

- **Case 3: 분할이 일어나는 삽입 과정**
  - **Case 3-1: 분할이 일어나는 노드가 리프 노드가 아닌 경우**
    - B트리와 동일하게 분할을 진행
    - 중간 Key를 부모 Key로 올리고, 분할할 두 개의 노드를 왼쪽, 오른쪽 자식으로 설정
  - **Case 3-2: 분할이 일어나는 노드가 리프 노드인 경우**
    - 중간 Key를 부모 Key로 올림
    - 오른쪽 노드에 중간 Key를 포함하여 분할
    - 왼쪽 자식 노드와 오른쪽 자식 노드를 이어줘 연결리스트 형태를 유지
       
      <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/B%2BTree-Insert3-1.jpg" width="600">
      <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/B%2BTree-Insert3-5.jpg" width="600">

## B+Tree 삭제 과정
  - 삭제시 트리의 Key가 변경되는 경우로 설명
  - B트리와 유사하지만 삭제하는 키 K는 무조건 리프 노드에 존재하며, 삭제를 위한 탐색 과정에서 K가 index에 존재할 수 있다는 점에서 차이가 있음
 
### 삭제 Case
- **Case 1: 삭제할 K가 index에 없고, 리프 노드의 가장 처음 key가 K가 아닌 경우**
  - **Case 1-1: 리프 노드의 Key 개수가 t-1보다 클 때**
    - B트리의 삭제 과정과 동일
    - 리프 노드의 Key만 삭제하고 종료
      
      <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/B%2BTree-Del1-1.jpg" width="600">

  - **Case 1-2: 리프 노드의 Key 개수가 t-1일 때**
    - B트리의 삭제 과정과 동일
    - **Case 1-2a: 형제 노드 중 하나라도 Key의 개수가 t-1보다 큰 경우 (빌려올 수 있는 경우)**
      - 왼쪽 노드가 큰 경우
        - 왼쪽 노드의 가장 큰 값을 현재 노드에 받고, 부모 노드의 Key도 바뀐 값으로 변경
      - 오른쪽 노드가 큰 경우
        - 현재 노드에 변화 없음
        - 우측 노드의 최솟값을 현재 노드로 옮기고 우측 노드의 부모 Key를 넘어간 최솟값의 다음 값으로 변경

    - **Case 1-2b: 형제 노드가 모두 t-1인 경우 (빌려올 수 없는 경우)**
      - 모든 경우에서 최소 차수를 만족할 수 없으므로 형제 노드들 중 하나와 병합
      - 왼쪽 노드와 병합
        - 현재 노드의 부모 Key 값 변경
      - 오른쪽 노드와 병합
        - 우측 노드의 부모 Key 값 변경
      - 부모 노드의 Key 개수가 1 감소한 경우 부모 노드의 Key 개수가 t-1 미만이면 재구성
        
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/B%2BTree-Del1.png" width="600">

- **Case 2: 삭제할 K가 리프노드의 가장 처음 Key인 경우(index에 K가 존재하는 경우)**
  - Key의 개수가 최소 Key의 개수일 때 형제 노드의 Key를 빌려오거나 부모 Key와 병합하는 등 과정은 B트리와 동일하게 수행
  - **Case 2-1: 리프 노드의 Key 개수가 t-1보다 클 때**
    - 리프 노드를 삭제하고 기존 Key가 있던 인덱스 노드 자리에 inorder successor(후계자) 값으로 변경
   
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/B%2BTree-Del2-1-1.jpg" width="600">
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/B%2BTree-Del2-1-2.jpg" width="600">

  - **Case 2-2: 리프 노드의 Key 개수가 t-1 일때**
    - **Case 2-2a: 형제 노드 중 하나라도 Key 개수가 t-1보다 큰 경우**
      - 왼쪽에서 빌려오는 경우
        - 현재 노드의 첫 번째 값이 바뀌므로 인덱스 노드의 Key 값도 빌려온 값으로 교체
      - 오른쪽에서 빌려오는 경우
        - 현재 노드의 우측 노드의 첫 번째 값이 바뀌므로 인덱스 노드의 기존 우측 노드 첫 번째 값을 다음 값으로 교체

      - **Case 2-2b: 형제 노드가 모두 t-1인 경우**
        - 형제 노드 중 하나와 현재 노드를 병합
          - 왼쪽 형제 노드와 병합한 경우
            - 현재 노드의 부모 Key를 삭제
          - 오른쪽 형제 노드와 병합한 경우
            - 오른쪽 노드의 부모 Key를 삭제
        - 부모 Key가 삭제되었으므로 부모 노드의 Key 개수가 t-1 미만이면 재구성

      <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/B%2BTree-Del2.png" width="600">

> ⬆️:[Top](#B-Tree)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#1-data-structure)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [[자료구조] 그림으로 알아보는 B+Tree](https://velog.io/@emplam27/자료구조-그림으로-알아보는-B-Plus-Tree)
> - [B+트리, B*트리(B+Tree, B*Tree)](https://8iggy.tistory.com/191)
> - [[자료구조] 간단히 알아보는 B-Tree, B+Tree, B*Tree](https://ssocoit.tistory.com/217)
