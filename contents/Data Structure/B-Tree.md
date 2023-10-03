# B-Tree
## 개념
  - 이진트리를 확장해 하나의 노드가 가질 수 있는 자식 노드의 최대 숫자가 2보다 큰 트리 구조
  - 외부 검색트리
    - 검색 트리가 외부(디스크)에 저장되어 있는 경우
  - 다진 검색트리
    - 검색트리의 분기수를 늘려 트리의 높이를 줄임
  - 트리의 균형을 유지하여 최악의 경우 디스크 접근 횟수를 줄임
    - CPU의 효율성보다 디스크의 접근 횟수가 효율을 좌우함
    - 이를 위해 높이를 낮추고 균형을 유지하여 디스크 접근 횟수를 줄임

## B-Tree의 특징
  1. 노드에는 2개 이상의 데이터(Key)가 들어갈 수 있으며, 항상 정렬된 상태로 저장한다
  2. 루트 노드와 리프 노드를 제외한 내부 노드는 M/2 ~ M개의 자식을 갖는다(최소 절반 이상은 갖는다)
     - 최대 M개의 자식을 가질 수 있는 B트리를 M차 B트리라고 한다
     - 루트 노드는 최소 2개의 자식을 갖는다
  3. 특정 노드의 데이터(Key)가 K개라면, 자식 노드의 개수는 K+1개여야 한다
  4. 특정 노드의 왼쪽 서브 트리는 특정 노드의 Key보다 작은 값들로, 오른쪽 서브 트리는 큰 값들로 구성된다
  5. 노드 내에 데이터는 floor(M/2)-1개부터 최대 M-1개까지 포함될 수 있다
  6. 최소 차수는 자식수의 하한 값을 의미하며, 최소차수가 t라면 M = 2t - 1을 만족
  7. 모든 리프 노드들이 같은 레벨에 존재한다
     
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTreeleaf.webp" width=500>

## B-Tree의 노드 구조
  - 하나의 페이지(블록)

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTreeNode.jpeg" width=500>
  
- B Tree에서의 M 값
  - Key와 분기 포인터 공간을 반영하여 디스크 한 블록이 수용할 수 있는 최대 값
 
- B Tree에서 레코드에 접근하는 과정
  - 블럭 포인터를 통해 키 값의 데이터에 접근
 
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTreeRecord.jpeg" width=500>

## B-Tree의 탐색 과정
  - B Tree는 루트 노드에서 탐색을 시작하여 하향식으로 탐색을 진행
    1. 루트 노드에서 탐색을 시작
    2. K를 찾았다면 탐색을 종료
    3. K와 노드의 Key 값을 비교해 알맞은 자식 노드로 내려간다
    4. 해당 과정을 리프 노드에 도달할 때까지 반복한다
    5. 리프 노드에서도 K를 찾지 못했다면 트리에 값이 존재하지 않는 것
   
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTreeSearch1.webp" width=500>
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTreeSearch2.webp" width=500>
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTreeSearch3.webp" width=500>
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTreeSearch4.webp" width=500>

## B-Tree의 삽입 과정
  - B Tree에 데이터를 삽입하는 과정은 탐색과는 달리 상향식으로 진행
  - 데이터 삽입은 항상 리프 노드에서 시작
    1. 트리가 비어있다면 루트 노드를 할당하고 K를 삽입
    2. 트리가 비어있지 않다면, 데이터를 넣을 적절한 리프 노드를 탐색
    3. 리프 노드에 데이터를 삽입 후 리프 노드가 적절한 상태에 있다면 종료
    4. 리프 노드가 부적절한 상태에 있다면 분리
       - 부적절한 상태: 데이터 오버플로우가 발생한 상황

### 삽입 Case
- **Case 1: 분리가 일어나지 않는 경우**
  1. 데이터를 삽입할 리프 노드를 탐색하고, 해당 노드에 데이터를 삽입
  2. 해당 노드가 적절한 상태이기에 삽입 종료
 
      <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTreeInsertCase1.jpeg" width=500>
  
- **Case 2: 분리가 일어나는 경우**
  1. 데이터를 삽입할 리프 노드를 탐색하고, 해당 노드에 데이터를 삽입
  2. 해당 노드의 왼쪽 키들은 왼쪽 자식으로, 오른쪽 키들은 오른쪽 자식으로 분리
  3. 부모 노드를 검사해 부모 노드가 부적절 상태에 있다면 위와 같은 분리를 반복
     
      <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTreeInsertCase2.jpeg" width=500>
      <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTreeInsertCase2-2.jpeg" width=500>
      <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTreeInsertCase2-3.jpeg" width=500>
     
## B-Tree의 삭제 과정
  - B Tree의 데이터 삽입 과정보다 복잡
  - 데이터 삭제 과정에서 B Tree의 조건에 문제가 생길 수 있음
    - 내부 노드는 M/2 ~ M개의 자식을 가질 수 있다
      - 최소 유지 개수를 충족시키지 못하는 문제가 발생 가능
    - 각 노드는 floor(M/2)-1 ~ M-1 개의 데이터(Key)를 가질 수 있다
      - 최소 유지 개수를 충족시키지 못하는 문제가 발생 가능
    - 노드의 Key가 K개 라면 자식 노드의 개수는 K+1개여야 한다
      - 최소 유지 개수를 충족시키지 못하는 문제가 발생 가능
  
### 삭제 Case
- 설명을 위해 임의의 용어 정의
  - Lmax: 현재 노드의 왼쪽 자식들 중 가장 큰 Key
  - Rmin: 현재 노드의 오른쪽 자식들 중 가장 작은 Key
  - Parent: 현재 노드를 가리키는 부모 노드의 자식 포인터 오른쪽에 있는 Key.
    - 마지막 자식 노드의 경우 부모의 마지막 Key
  - K: 삭제할 Key

- **Case 1: 리프 노드에서 삭제되는 경우**
  - **Case 1-1: 값을 삭제하더라도 최소 유지 개수 조건을 만족하는 경우**
    - 최소 유지 개수를 만족하므로 바로 삭제
 
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase1-1.webp" width=500>
          
  - **Case 1-2: 최소 유지 개수를 만족하지 못하지만 바로 옆 형제 노드들에게 값을 빌려올 수 있는 경우**

    1\. K와 Parent를 바꿈
        
    2-1. 왼쪽 형제 노드에서 빌려올 수 있다면 Lmax와 Parent를 바꿈

    2-2. 오른쪽 형제 노드에서 빌려올 수 있다면 Rmin과 Parent를 바꿈
    - 둘 다 수행이 가능할 경우 둘 중 하나를 선택하여 수행
   
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase1-2-1.webp" width=500>
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase1-2-2.webp" width=500>
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase1-2-3.webp" width=500>
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase1-2-4.webp" width=500>
     
  - **Case 1-3: 최소 유지 개수를 만족하지 못하고 형제 노드에게 값을 빌려올 수 없지만 부모 노드를 분할할 수 있는 경우**
    - K를 삭제하고 Parent를 부모 노드에서 분할하여 형제 노드에 병합
       
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase1-3-1.webp" width=500>
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase1-3-2.webp" width=500>
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase1-3-3.webp" width=500>

  - **Case 1-4: 최소 유지 개수를 만족하지 못하고 형제 노드에게 값을 빌려올 수 없고 부모 노드도 분할할 수 없는 경우**
    - 모든 노드의 개수가 최소인 경우로 Case 2-2와 동일
          
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase1-4.jpeg" width=500>
        <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase1-4-2.jpeg" width=500>
    
- **Case 2: 리프 노드가 아닌 내부 노드에서 삭제되는 경우**
  - **Case 2-1: 현재 노드 혹은 자식 노드의 최소 유지 개수의 최소보다 큰 경우**
        
    1\. K의 Lmax 혹은 Rmin과 자리 교체
        
    2\. 이후 리프 노드의 삭제 케이스와 동일하게 수행
   
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase2-1-1.webp" width=500>
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase2-1-2.webp" width=500>

  - **Case 2-2: 현재 노드와 자식 노드 모두 Key 개수가 최소인 경우**

    1\. K를 삭제하고 K의 자식을 하나로 합침
           
    2\. K의 Parent를 K의 형제 노드에 합침
           
    3\. N1을 N2의 자식이 되도록 연결
           
    4-1. 만약 N2의 Key 개수가 최대보다 크다면 Key 삽입 과정과 동일하게 분할
        
    4-2. 만약 N2의 Key 개수가 최소보다 작다면 2번 과정으로 돌아가 동일한 과정 반복

    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase2-2-1.webp" width=500>
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase2-2-2.webp" width=500>
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTree-delCase2-2-3.webp" width=500>

## B Tree의 시간복잡도
  - 탐색/삽입/삭제 연산의 수행 시간은 `O(log n)`
  - 균형잡힌 BST와 동일한 시간 복잡도를 가지지만 BST에 비해 상수인자가 적음
    - B 트리가 BST보다 상수 시간만큼 더 빠르다

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BTreeTime.jpeg" width=500>

> ⬆️:[Top](#B\-Tree)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#-Data-Structure)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[자료구조] B-트리(B-Tree)란? B트리 그림으로 쉽게 이해하기, B트리 탐색, 삽입, 삭제 과정](https://code-lab1.tistory.com/217)
