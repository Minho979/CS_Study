# Tree
## Tree의 개념

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/Tree.png" width="500">

  - 트리는 노드 구조로 이루어진 자료구조
    1. 트리는 하나의 루트 노드를 가짐
    2. 루트 노드는 0개 이상의 자식 노드를 가짐
    3. 자식 노드 또한 0개 이상의 자식 노드를 가지며, 이는 반복적으로 정의됨
  - 노드(node)들과 노드들 사이를 연결하는 간선(edge)들로 구성
    - 트리에는 사이클(cycle)이 존재 불가
    - 노드들은 특정 순서로 나열될 수도 있고 그럴 수 없을 수도 있음
    - 각 노드는 부모 너드로의 연결이 있을 수도 있고 없을 수도 있음
    - 각 노드는 어떤 자료형으로도 표현 가능
  - 비선형(1:n) 자료구조로 계층적 관계를 표현
    - 예) 디렉터리 구조, 조직도, 가계도
  - 그래프의 한 종류
    - 사이클(cycle)이 없는 하나의 연결 그래프(Connected Graph)
    - DAG(Directed Acyclic Graph, 방향성이 있는 비순환 그래프)의 한 종류
    - 최소 신장 트리(MST, Minimum Spanning Tree)라고도 불림

## Tree의 종류
### 이진 트리 (Binary Tree)
    
![BinaryTree](https://github.com/Minho979/CS_Study/blob/main/contents/images/BinaryTree.png)

- Tree의 차수를 2이하가 되도록 제한한 트리
  - 왼쪽, 오른쪽 자식 노드만을 가지도록 제한
- 이진 트리가 아닌 트리도 이진 트리로 변환하여 다룰 수 있음
      
![general-binary](https://github.com/Minho979/CS_Study/blob/main/contents/images/general-binaryTree.png)

- 재귀적 구성

  ![subTree](https://github.com/Minho979/CS_Study/blob/main/contents/images/subTree.png)
  
  - 루트 노드의 왼쪽 자식 노드를 루트로 하는 서브트리도 이진트리
  - 루트 노드이 오른쪽 자식 노드를 루트로 하는 서브트리도 이진트리
  - 공백 트리 또한 이진트리
    - 노드 수가 N인 경우 간선의 수는 N-1개
    - 높이가 h인 경우 가질 수 있는 노드 수는 $(h+1)$ ~  $(h ^{h+1} -1)$

#### 이진 트리의 종류
- **포화 이진 트리(Full Binary Tree)**
  - 모든 레벨에서 최대 개수의 노드를 가진 이진 트리
- **완전 이진 트리(Complete Binary Tree)**

  ![completebinarytree](https://github.com/Minho979/CS_Study/blob/main/contents/images/completebinarytree.png)

  - 높이가 h일 때, 레벨 0부터 h-1 까진 포화 상태이고 h레벨에서는 왼쪽부터 차례대로 노드가 채워진 이진 트리
  - 포화 이진 트리도 완전 이진 트리의 한 종류

- **편향 이진 트리(Skewed Binary Tree)**

  ![skewedbinarytree](https://github.com/Minho979/CS_Study/blob/main/contents/images/skewedbinarytree.png)

  - 높이 h에 대한 최소 노드 개수(h+1)를 가지면서 한쪽 방향 자식 노드만을 가진 이진 트리
    - 좌편향 이진 트리, 우편향 이진 트리로 나뉨

#### 이진 트리의 순회(traversal)
- **전위 순회(Pre-order traversal)**
  1. 현재 노드 T를 방문하여 처리: D
  2. 현재 노드 T의 왼쪽 서브트리를 전위 순회: L
  3. 현재 노드 T의 오른쪽 서브트리를 전위 순회: R
  - D-L-R 순서로 진행
       
![preoredr](https://github.com/Minho979/CS_Study/blob/main/contents/images/Tree%20preorder.png)

- **중위 순회(in-order traversal)**
  1. 현재 노드 T의 왼쪽 서브트리를 중위 순회: L
  2. 현재 노드 T를 방문하여 처리: D
  3. 현재 노드 T의 오른쪽 서브트리를 중위 순회: R
  - L-D-R 순서로 진행하며, 빈공간이 있을 시 빈공간에 노드가 있다고 가정하고 순회함
   
![inoredr](https://github.com/Minho979/CS_Study/blob/main/contents/images/Tree-inorder.png)

- **후위 순회(post-order traversal)**
  1. 현재 노드 T의 왼쪽 서브트리를 후위 순회: L
  2. 현재 노드 T의 오른쪽 서브트리를 후위 순회: R
  3. 현재 노드 T를 방문하여 처리: D
  - L-R-D 순서로 진행
          
![postoredr](https://github.com/Minho979/CS_Study/blob/main/contents/images/tree-postorder.png)


### 이진 탐색 트리 (Binary Search Tree)
- 시간 복잡도를 O(n) -> O(log n)으로 줄일 수 있음
- 이진 트리에 탐색을 위한 조건을 추가한 자료구조
  1. 모든 원소는 유일한 Key를 가진다
  2. 왼쪽 서브트리 원소들의 Key는 그 루트의 Key보다 작다
  3. 오른쪽 서브트리 원소들의 Key는 그 루트의 Key보다 크다
  4. 왼쪽 서브트리와 오른쪽 서브트리도 이진 탐색 트리이다
- 원소의 수가 아닌 트리 높에 비례한 시간이 소요
#### 이진 탐색 트리의 연산
**검색**
- 루트에서 시작하여 특정 키 값을 찾는 연산
- 서브트리에 대해 재귀적으로 검색 연산 반복
  - key = 루트 노드의 경우
    - 즉시 연산 종료
  - key < 루트 노드의 경우
    - 루트 노드의 왼쪽 서브트리에 대해 검색 연산 수행
  -  key > 루트 노드의 경우
    - 루트 노드의 오른족 서브트리에 대해 검색 연산 수행
        
  ![TreeSearch](https://github.com/Minho979/CS_Study/blob/main/contents/images/tree-search.png)
        
**삽입**
- 특정 키 값을 삽입하는 연산
- 먼저 검색을 실행하고 검색 실패시 검색 실패한 위치에 삽입을 수행
  - 검색이 성공할 시 원소의 유일성이 깨지므로 수행하지 않음
  - 검색 실패 시 삽입 가능
    - 검색 과정은 원소를 삽입할 위치를 찾는 과정이기도 함
      
![TreeInsert](https://github.com/Minho979/CS_Study/blob/main/contents/images/tree-insert.png)

**삭제**
- 특정 키를 삭제하는 연산
- 검색을 수행하고 검색 성공 시 해당 노드 삭제
  - [case1] 삭제할 노드가 단말 노드인 경우
    - 해당 노드만 삭제
              
      ![TreeDelCase1](https://github.com/Minho979/CS_Study/blob/main/contents/images/tree-del-case1.png)

  - [case2] 삭제할 노드가 하나의 자식 노드를 가진 경우 (후속처리 필요)
    - 해당 노드 삭제 후 삭제된 노드의 자리를 자식 노드가 위치하게 한다
              
      ![TreeDelCase2](https://github.com/Minho979/CS_Study/blob/main/contents/images/tree-del-case2.png)

  - [case3] 삭제할 노드가 두개의 자식 노드를 가진 경우 (후속처리 필요)
    - 해당 노드 삭제 후 자식 노드 중 후계자를 선택하여 위치하게 한다
      - 왼쪽 서브트리에서 가장 큰 노드
        - 오른쪽 링크 필드가 null인 노드를 후계자 노드로 선정할 수 있음
      - 오른쪽 서브트리에서 가장 작은 노드
        - 왼쪽 링크 필드가 null인 노드를 후계자 노드로 선정할 수 있음
                  
          ![TreeDelCase3](https://github.com/Minho979/CS_Study/blob/main/contents/images/tree-del-case3.png)

        - 삭제 후 이진 탐색 트리 유지를 위해 이진 탐색 트리의 재구성 과정(후속 처리)이 필요

#### 연산의 시간 복잡도
- 노드 수가 n, 높이가 h인 경우 삽입/삭제/검색 시간은 O(h)
  - 좌우 균형이 맞는 경우 O(log n)
  - 편향 이진 트리의 경우 O(n)
  - 높이를 낮게 유지할 수록 시간 복잡도가 낮아짐

### 균형 트리 (Balance Binary Search Tree)
- 오른쪽 서브트리의 높이와 왼쪽 서브트리의 높이의 차가 1이하인 이진 탐색 트리
  - 이 높이 차이를 균형인수(Balance factor)라고 부름
- 모든 연산에 O(log n)의 시간이 걸림
- 자료의 삽입,삭제가 잦은 경우 균형 유지를 위한 재배치 오버헤드가 성능을 저하시킬 수 있음
- AVL Tree, Red-Black Tree, B Tree, B+ Tree 등이 있음

### 이진 힙 (Binary Heap)
    
![binaryHeap](https://github.com/Minho979/CS_Study/blob/main/contents/images/Heap.png)
    
- Key 값이 가장 크거나 작은 노드를 쉽게 찾기 위해 만들어진 완전 이진 트리
- n개의 노드의 힙에서 삽입/삭제 연산의 시간 복잡도는 O(log n)
- 최대 힙(Max Heap)
  - Key 값이 가장 큰 노드를 빠르게 찾기 위한 자료구조
  - 완전 이진 트리
    - 부모 노드의 Key 값 ≥ 자식 노드의 Key 값
    - Key 값이 가장 큰 노드가 루트 노드
- 최소 힙(Min Heap)
  - Key 값이 가장 작은 노드를 빠르게 찾기 위한 자료구조
  - 완전 이진 트리
    - 부모 노드의 Key 값 ≤ 자식 노드의 Key 값
    - Key 값이 가장 작은 노드가 루트 노드

## 이진 탐색 트리(Binary Search Tree) vs 최대 힙(Max Heap)
  ||이진 탐색 트리|최대 힙|
  |:---:|---|---|
  |이진 트리|O|O|
  |트리의 균형|X(균형이 안맞을 수 있음)|O(항상 완전 이진 트리)|
  |특정 키값 검색|O|X(최대 값 빠르게 찾기, 특정 검색 X)|
  |같은 값의 원소|X(키 값은 유일해야 함)|O(동일 값 허용)|
  |우선순위 큐|X(부적합)|O(오름차순 정렬, 중복값 허용)|
  |삽입/삭제 연산|O|O|
  |오름차순 출력|O(중위 순회)|X|

## Tree의 특징
  - 그래프의 한 종류로 '최소 신장 트리(MST, Minimum Spanning Tree)'라고도 불림
  - Tree는 계층 모델
  - Tree는 DAG(Directed Acyclic Graph, 방향성이 있는 비순환 그래프)의 한 종류
    - loop나 circuit이 없으며 self-loop도 없음
    - 사이클이 존재하지 않음
  - 노드가 N개인 트리는 항상 N-1개의 간선(edge)를 가짐
    - 간선은 항상 (정점의 개수 - 1)개를 가짐
  - 루트에서 어떤 노드로 가는 경로는 유일
    - 임의의 두 노드 간 경로도 유일
    - 두 개의 정점 사이에 반드시 1개의 경로만을 가짐
  - 한 개의 루트 노드만이 존재하며 모든 자식 노드는 한 개의 부모 노드만을 가짐
    - 부모-자식 관계이므로 흐름은 top-bottom 혹은 bottom-top
  - 순회는 Pre-order, In-order 혹은 Post-order로 이루어짐
    - 3가지 모두 DFS/BFS 안에 속함
  - 트리는 이진 트리(Binary Tree), 이진 탐색 트리(Binary Search Tree), 군형 트리(AVL 트리, Red-Black 트리 등), 이진 힙(최대힙, 최소힙) 등이 있음

> ⬆️:[Top](#1-DataStructure)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#1-data-structure)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [이지영. 지바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[자료구조] 트리(Tree)란](https://gmlwjd9405.github.io/2018/08/12/data-structure-tree.html)
