# Binary Heap
## Heap의 개념
  - 완전 이진 트리의 일종으로 우선순위 큐를 위해 만들어진 자료구조
    - 선형자료구조의 경우 자료의 위치에 따라 시간이 상이함 O(1) ~ O(n)
    - 힙의 경우 자료의 위치와 관계 없이 시간이 O(log n)으로 항상 일정
  - 여러 개의 값들 중에서 최대값이나 최소값을 빠르게 찾아내는 자료구조
  - 힙은 일종의 반정렬 상태(느슨한 정렬 상태)를 유지
    - 큰 값이 상위 레벨에 있고 작은 값이 하위 레벨에 있다는 정도(최대힙)
    - 간단히 부모 노드의 키 값이 자식 노드의 키 값보다 항상 큰(작은) 이진 트리를 의미
  - 힙 트리에서는 중복된 값을 허용 (이진 탐색 트리에서는 중복된 값을 허용하지 않음)

## Heap의 종류
**최대 힙(Max Heap)**
- 부모 노드의 키 값이 자식 노드의 키 값보다 크거나 같은 완전 이진 트리
- 부모 노드의 Key 값 ≥ 자식 노드의 Key 값

**최소 힙(Min Heap)**
- 부모노드의 키 값이 자식 노드의 키 값보다 작거나 같은 완전 이진 트리
- 부모 노드의 Key 값 ≤ 자식 노드의 Key 값

  ![binaryHeap](https://github.com/Minho979/CS_Study/blob/main/contents/images/Heap.png)

## Heap의 구현
  - Heap을 저장하는 표준적인 자료구조는 배열
    - 완전 이진 트리로 메모리 낭비가 없고 빠르게 검색이 가능하기에 1차원 배열 사용
  - 특정 위치의 노드 번호는 새로운 노드가 추가되어도 변하지 않음
  - 부모 노드와 자식 노드의 관계
    - 왼쪽 자식 노드의 인덱스 = (부모의 인덱스) * 2
    - 오른쪽 자식 노드의 인덱스 = (부모의 인덱스) * 2 + 1
    - 부모의 인덱스 = (자식의 인덱스)/2
## Heap의 연산
**삽입**

1. 완전 이진 트리를 유지하면서 노드를 확장하여 삽입할 원소를 임시 저장
   - 노드가 n개인 완전 이진 트리에서 다음 노드의 확장 자리는 n+1번의 노드가 됨
   - n+1번 자리에 노드를 확장하고 그 자리에 삽입할 원소를 임시 저장
2. 만들어진 완전 이진 트리 내에서 삽입 원소의 제자리를 찾는다
   - 현재 위치에서 부모 노드와 비교하여 크기 관계를 확인
   - (현재 부모 노드의 키 값 ≥ 삽입 원소의 키 값)의 관계가 성립하지 않으면, 현재 부모 노드의 원소와 삽입 원소의 자리를 서로 바꿈
- 노드 수가 n 일때 연산 시간 복잡도는 O(log n)

    ![Max Heap_insert](https://github.com/Minho979/CS_Study/blob/main/contents/images/MaxHeap.gif)
    ![Max Heap_insert1](https://github.com/Minho979/CS_Study/blob/main/contents/images/heap_insert_case1.png)
    ![Max Heap_insert2](https://github.com/Minho979/CS_Study/blob/main/contents/images/Heap_insert_case2.png)

    
**삭제**
- 힙에서는 루트 노드의 원소만을 삭제 가능
  - 최대값 또는 최소값 원소가 정렬 기준에 따라 루트에 위치하고 있다
1. 루트 노드의 원소를 삭제하여 반환
2. 원소의 개수가 n-1개로 줄었으므로 노드의 수가 n-1인 완전 이진 트리로 조정
   - 노드가 n개인 완전 이진 트리에서 노드 수 n-1인 완전 이진 트리가 되기 위해서 마지막 노드, 즉 n번 노드를 삭제해야 함 
   - 삭제된 n번 노드에 있던 원소는 비어있는 루트 노드에 임시 저장
3. 완전 이진 트리 내에서 임시 저장된 원소의 제자리를 찾는다
   - 현재 위치에서 자식 노드와 비교하여 크기 관계를 확인
   - (임시 저장한 원소의 키 값 ≥ 현재 자식 노드의 키 값)의 관계가 성립하지 않으면, 현재 자식 노드의 원소와 임시 저장한 원소의 자리를 서로 바꿈
- 노드 수가 n일때 연산 시간 복잡도는 O(log n)
   
    ![Max Heap-del](https://github.com/Minho979/CS_Study/blob/main/contents/images/MaxHeap-Del.gif)
    
    ![Max Heap_del](https://github.com/Minho979/CS_Study/blob/main/contents/images/Heap_del.png)

> ⬆️:[Top](#BinaryHeap)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#1-data-structure)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [이지영. 지바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [Heap Data Structures](https://www.tutorialspoint.com/data_structures_algorithms/heap_data_structure.htm)
