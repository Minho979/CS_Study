# LinkedList
## LinkedList의 개념

- 각 노드가 데이터와 포인터를 가지고 연결되어 있는 방식으로 데이터를 저장
- 노드는 data 필드와 link 필드로 구성
      
  ![노드 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/Node.png)
  
  - data 필드: 원소 값을 저장, 원소의 형태에 따라 하나 이상의 필드로 구성
  - link 필드: 다음 노드의 주소 저장, 마지막 노드는 null을 저장

- 여러 개의 작은 공간을 연결하여 전체의 자료구조를 형성
- 자료의 논리적인 순서와 물리적인 순서가 불일치

<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/LinkedList2.png" width="400">
<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/LinkedList1.png" width="400">

  - 접근, 탐색의 시간 복잡도: O(n)
    - 인덱스 i의 노드의 접근할 시 Head에서 i번 이동 / 탐색 시 Array와 동일하게 첫 노드부터 선형 탐색을 진행 
  - 삽입, 삭제의 시간 복잡도: O(1)
    - 삽입, 삭제할 노드의 주변 노드의 Link만 수정

## LinkedList의 종류

연결 방식에 따라 구분

#### 단순 연결 리스트 (singly linked list)

  
  ![단순 연결 리스트 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/SLinkedList.png)
    
  - 노드에 링크 필드가 하나이며, 링크 필드를 통해 다음 노드와 연결되는 구조
  - 첫번째 노드를 모를 시 접근이 불가능하며, 첫 노드를 알면 모든 노드에 접근 가능
      
#### 원형 연결 리스트 (circular linked list)

  
  ![원형 연결 리스트 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/CLinkedList.png)
    
  - 단순 연결 리스트에서 마지막 노드가 리스트의 첫번째 노드와 연결되어 리스트를 원형으로 구성
      
#### 이중 연결 리스트 (doubly linked list)

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/DLinkedListNode.png" width="100" height="50">
    
  - data 필드와 두 개의 link 필드로 구성
  
    ![이중 연결 리스트 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/CDLinkedList.png)

## Linked List 연산 
#### 노드 삽입
- Node A와 C 사이에 B를 삽입하고자 할 때, B가 C를 가리키게 한 후, A가 B를 가리키게 한다.
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/LinkedList-Insert.png" width="500">
#### 노드 삭제
- Node A, B, C가 차례로 연결되어 있을 때 B를 삭제하는 경우 A가 C를 가리키게한 후 Node B를 삭제한다.
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/LinkedList-Del.png" width="500">
> ⬆️:[Top](#LinkedList)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#-Data-Structure)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [이지영. 지바로 배우는 쉬운 자료구조. 한빛아카데미]
