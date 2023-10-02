# Red-Black Tree
## 개요
  - BST(Binary Search Tree)의 검색, 삽입, 삭제 연산의 시간복잡도는 O(h) (h는 트리의 높이)
  - 편향 이진트리의 경우 h=n이 되며 O(n)의 시간 복잡도를 가짐
  - BST에 데이터가 random하게 구성될 경우 평균 트리의 높이는 log n으로 O(log n)의 시간복잡도를 가짐
  - Tree의 밸런스를 유지하면서 최악의 경우에도 O(log n)의 시간복잡도를 갖게하기 위해 고안

## 개념
  - Binary Search Tree의 일종
  - 항상 균형잡힌 트리 상태를 유지하여 높이가 log n
    - 완벽하게 균형이 맞다는 것이 아니라 높이의 차이가 2배 이내
  - 검색, 삽입, 삭제 연산을 최악의 경우에도 O(log n) 시간복잡도를 지원
    - 삽입, 삭제의 알고리즘을 수정하여 항상 트리의 균형을 유지하도록 함
  - 각 노드는 하나의 키(Key), 왼쪽 자식(Left), 오른족 자식(Right), 부모노드(p)의 주소를 저장
  - 자식 노드가 없는 경우 NIL 노드라는 특수한 노드가 있다고 가정
    - 모든 리프노드는 NIL 노드
  - 노드들은 내부노드와 NIL 노드로 분류
    - 실제 구현시 NIL 노드는 포함하지 않음
    - 개념을 쉽게 정의하기 위해 가상적으로 NIL 노드 사용

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/red-black1.jpeg" width="600">

## 조건
  1. 각 노드는 red 혹은 black
  2. 루트 노드는 black
  3. NIL 노드는 전부 black
  4. red 노드의 자식 노드들은 black (red 노드는 연속해서 등장할 수 없음)
  5. 모든 노드에 대해 그 노드로 부터 자손인 리프 노드(NIL 노드)에 이르는 모든 경로에는 동일한 개수의 black 노드가 존재

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/red-black2.png" width="500">

## Red-Balck Tree의 높이
  - 노드 x의 높이 h(x)는 자신으로부터 NIL 노드까지의 가장 긴 경로에 포함된 edge(간선)의 개수
  - 노드 x의 블랙-높이 bh(x)는 x로부터 NIL 노드까지의 경로상의 블랙 노드의 개수 (노드 x 자신은 미포함)
  - 높이가 h인 노드의 블랙-높이 bh ≥ (h/2)
    - 조건 4에 의해 레드 노드는 연속될 수 없기에 블랙 노드의 수가 높이의 절반 이상
  - 노드 x를 루트로 하는 임의의 서브트리는 적어도 $2^{bh(x)}-1$개의 내부노드를 포함(수학적 귀납법)
  - 위의 두 가지 증명으로 n개의 내부노드를 가지는 red-black tree의 높이는 2log(n+1) 이하
    - $n ≥ 2^{bh}-1 ≥ 2^{h/2}-1$ (bh: 루트 노드의 블랙-높이, h: 루트 노드의 높이)
  - 5가지 조건을 만족하는 red-black tree라면 자동으로 높이는 O(log n)

## Left and Right Rotation

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/red-black-rotation.png" width="500">
  
  - 삽입과 삭제 연산이 필요로 하는 Left,Right Rotation 연산
  - 한 노드를 중심으로 회전하여 부분적으로 트리의 모양을 수정하는 연산
  - 이진 탐색 트리(BST)의 특성을 유지
    - Rotate(회전)를 해서 서브트리가 옮겨지더라도, BST의 특성은 유지 
  - x와 y의 자식들은 모두 서브트리
  - 연산의 시간 복잡도는 O(1)

### Left Rotation
- y = right[x] =! NIL 가정 (a != b a는 b와 같지 않다, a =! b a = !b)
- 루트 노드의 부모도 NIL 가정

### pseudo code(의사 코드)
``` java
      LEFT-ROTATE(T, x)
      01  y <- right[x]        // x의 오른쪽 자식 노드를 y에 저장
      02  right[x] <- left[y]  // x의 오른쪽 자식 노드를 y의 왼쪽 자식 노드로 설정
      03  p[left[y]] <- x      // y의 왼쪽 자식 노드의 부모 노드를 x로 만드는 link 연결
      04  p[y] <- p[x]         // y의 부모 노드를 현재 x부모 노드로 할당
      05  if p[x] = NIL[T]     // x가 루트인 경우
      06    then root[T] <- y  // y를 루트로 설정정
      07    else if x = left[p[x]]  // x의 부모 노드가 존재하고 x가 왼쪽 자식인 경우
      08      then left[p[x]] <- y  // y를 x의 부모 노드의 왼쪽 자식 노드로 설정
      09      else right[p[x]] <- y // 그렇지 않은 경우 y는 x의 부모 노드의 오른쪽 자식으로 설정
      10  left[y] <- x         // x를 y의 왼쪽 자식으로 설정
      11  p[x] <- y            // y가 x의 부모노드가 되도록 설정
```
  - 순서대로 수행하기에 시간복잡도는 O(1)

## Red-Black Tree의 연산
### 삽입(Insert)
  - BST에서 삽입 방법으로 노드를 삽입
  - 새로 삽입된 노드 x를 red로 변경
    - 비어있는 트리에 처음 삽입되는 노드는 루트 노드이므로 블랙으로 설정
  - x이 부모노드 p의 색상이
    - black이면 아무 문제가 발생하지 않음
    - red이면 red-black 특성 4번에 위배되어 조정이 필요
    - p가 red인 경우만 고려

### pseudo code
``` java
  RB-INSERT(T, x) 
  01 b <- nil[T]        // a의 한 칸 뒤를 쫒아 내려오는 포인터, insert 자리 괸리를 위함, NIL노드를 사용하지만 실제 구현시 null
  02 a <- root[T]       // 루트노드 포인터
  03 while a != nil[T]  // 루트 노드가 NIL이 아닌 경우 반복문 실행(새로운 노드 x가 들어갈 자리 찾기)
  04   do b <- a        // b에 루트 노드 저장
  05     if key[x] < key[a]  // 삽입 노드 < 루트 노드
  06       then a <- left[a]  // a에 a의 왼쪽 자식 노드 저장 -> a 갱신, 이때 b도 갱신됨
  07       else a <- right[a]  // 삽입 노드 > 루트 노드이면 a에 a의 오른쪽 자식 노드 저장 
  08 p[x] <- b        // x의 부모 노드를 b로 변경
  09 if b = nil[T]    // 루트 노드 b가 NIL이면 (예외적인 경우 b가 null인 경우)
  10   then root[T] <- x  // x를 루트 노드로 변경 
  11   else if key [x] < key[b]  // x 데이터 < 루트 노드 데이티
  12     then left[b] <- x  // b의 왼쪽 자식 노드를 x로 변경
  13     else right[b] <- x  //  x 데이터 > 루트 노드 데이터, b의 오른쪽 자식 노드를 x로
  14 left[x] <- nil[T]  // 14-15 새로운 노드는 BST의 leaf 노드이기에 새로운 노드의 자식들을 null로 설정
  15 right[x] <- nil[T]
  16 color[x] <- RED  // 삽입된 노드의 색을 RED로 설정
  17 RB-INSERT_FIXUP(T, z)  // 특성 중 위반되는게 있는지 확인하고 조정하기 위해 호출
``` 

### 조정 (RB-INSERT-FIXUP)
  
**레드블랙트리의 규칙이 위반될 가능성이 있는 조건**
    
- 각 노드는 red 혹은 black
  - 위반 가능성 없음
- 루트 노드는 black
  - 새로운 노드 x가 루트 노드라면 규칙 위반, 아니라면 위반 가능성 없음
  - 새로운 노드 x가 루트 노드라면 간단하게 노드를 블랙으로 바꾸는 작업을 수행하여 해결
- 모든 leaf 노드(NIL 노드)는 black
  - 새로운 노드의 자식들은 NIL 노드로 설정하기에 위반 가능성 없음
- red 노드의 자식 노드들은 전부 black(red 노드는 연속해서 등장 불가)
  - 위반 가능성 존재
    - 부모 노드가 red 노드였다면 RED-RED가 되므로 위반 발생
  - RED-RED 조건을 위반하는 것이 가장 큰 문제
- 모든 노드에 대해 그 노드로 부터 자손인 리프 노드(NIL 노드)에 이르는 모든 경로에는 동일한 개수의 black 노드가 존재
  - 새로운 노드를 RED로 추가 했으므로 위반 가능성 없음

**Loop Invariant(루프를 돌면서 변하지 않고 유지되는 조건)**
  
  - x는 red 노드
  - 오직 하나의 위반만이 존재
    - 조건 2: x가 루트 노드이면서 red
    - 조건 4: x와 그 부모 p[x]가 둘 다 red
      - 조건 4를 해결하기 위해 부모 노드를 타고 올라가다 보면, 또다른 RED-RED 위반이 있을 수 있음. 최악의 경우 루트 노드까지 타고 올라가게 되면, 조건 2를 위반한 것이므로 루트 노드를 블랙으로 바꿔주고 종료

**종료 조건**
  
  - 부모 노드 p[x] black이 되면 종료
  - 조건 2가 위반일 경우 x를 블랙으로 바꿔주고 종료

### Case 정리
  - 총 6가지 Case로 문제를 정의
  - p[p[x]]가 반드시 존재하는 이유는 RED-RED 위반이 발생한 경우, p[x]가 RED이므로 레드블랙트리의 조건에 의해 부모인 p[p[x]]는 블랙 노드로 존재
    - Case 1, 2-1, 2-2는 p[x]가 p[p[x]]의 왼쪽 자식인 경우
    - Case 3, 3-1, 3-2는 p[x]가 p[p[x]]의 오른쪽 자식인 경우
    - Case 1, 2-1, 2-2와 3, 4-1, 4-2은 대칭적, 코드상에서 left와 right만 바꿔주면 됨
    - Case 1, 2-1, 2-2에 대해서만 다룸

  - **Case 1: x의 부모의 형제가 RED인 경우**
    - 새로운 노드 x의 부모가 RED이면서, 부모의 형제 노드 s가 RED인 경우
    - 이 경우 부모 노드와 부모 노드의 형제 노드를 BLACK으로 바꾸고, 할아버지 노드를 RED로 바꾼다
    - 그 뒤, 할아버지 노드 $p^2$를 새로운 노드 x로 설정하여 위로 타고 올라가면서 레드블랙트리의 조건을 위반하는지를 검사
    - Case 1의 경우 문제가 완전히 해결되지 않았다. x가 두 칸 위로 올라가서 해당 위치부터 재귀적으로 해결해야 함
      - $p^2$의 부모가 블랙이면 삽입연산이 완료되지만 레드일 경우 재귀적으로 해결해야 함
    
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-InsertCase1.jpeg" width="600">
      
  - **Case 2: x의 부모의 형제가 BLACK인 경우**
    - x의 부모의 형제가 BLACK인 경우 실제로 BLACK 노드일 수도 있고, NIL 노드일 수도 있다
    - **Case 2-1: x가 오른쪽 자식인 경우**
      - p[x]에 대해서 left-rotation한 후 원래 p[x]를 x로 변경
      - Case 2-2로 이동
      
      <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-InsertCase2-1.jpeg" width="600">

    - **Case 2-2: x가 왼쪽 자식인 경우**
      - p[p[x]]에 대해 right-rotation을 진행
      - p[x]를 BLACK, p[p[x]]를 RED로 변경

      <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-InsertCase2-2.jpeg" width="600">

  - **Case 1, 2-1, 2-2 요약**
    - Case 1의 문제를 해결하고 나면 문제가 종료되지 않는다. Case 2-1, Case 2-2의 문제가 발생할 수 있으며, Case 1의 문제가 반복해서 발생할 수도 있다. 최악의 경우 루트 노드까지 올라가게 되어 레드블랙트리의 조건 2 루트 노드가 레드인 경우를 블랙으로 변경하면서 종료
    - Case 2-1은 Case 2-2를 거쳐서 해결하면 종료
    - Case 2-2의 경우 x의 할아버지 노드를 기준으로 right-rotate하면 문제가 해결되고 종료
    - Case 1, 2-1, 2-2의 경우에 해당하는 내용이며, Case 1에서 Case 3, 4-1, 4-2로 넘어갈 수도 있음
      
  - **Case 3, 4-1, 4-2**
    - Case 1, 2-1, 2-2는 p[x]가 p[p[x]]의 왼쪽 자식인 겅우
    - Case 3, 4-1, 4-2는 p[x]가 p[p[x]]의 오른쪽 자식인 경우
      - Case 1, 2-1, 2-2와 대칭
      - Case 1, 2-1, 2-2의 정리가 Case 3, 4-1, 4-2에 매칭
      - Case 3의 문제를 해결하고 나면 문제가 완전히 해결도니 것이 아니며 Case 3를 재귀적으로 다시 수행할 수도 있고, Case 4-1 4-2로 넘어가거나 Case 1, 2-1, 2-2로 넘어갈 수 있다. 이 과정은 2칸씩 올라가면서 해결
      - Case 4-1의 경우 Case 4-2를 거쳐서 해결 후 종료

### RB-INSERT-FIXUP Pseudo Code
```java
    RB-INSERT-FIXUP(T, x)          // x는 새로운 노드
    01 while color[p[x]] = RED      // x의 부모가 RED인 동안 RED-RED 위반, 탈출조건은 color[p[x]] = RED && p[x] != null (p[x] = BLACK) 
    02   do if p[x] = left[[p[x]]]  // x의 할아버지 노드의 왼쪽자식이 p[x]인 경우
    03     then b <- right[p[p[x]]] // 부모의 형제를 b에 저장
    04       if color[b] = RED      // b노드의 색상에 따라 CASE 구분 
    05         then color[p[x]] <- BLACK  >> CASE 1    // 부모 RED -> BLACK
    06              color[b] <- BLACK     >> CASE 1    // 부모 형제 RED -> BLACK
    07              color[p[p[x]]] <-RED  >> CASE 1    // 조부모 BLACK -> RED
    08              x <- p[p[x]]                       // 조무모 노드를 다시 x로 설정하여 트리를 타고 올라가면서 문제 해결 (포인터 2단계 상승 이동)
    09       else if x =  right[p[x]]  // 부모 RED, 부모 형제 BLACK, x가 p 오른쪽 자식
    10          then x <- p[x]          >> CASE 2-1   // 부모 노드를 x로 설정(포인터 1단계 상승 이동)
    11            LEFT-ROTATE(T, x)     >> CASE 2-1   // LEFT-ROTATE 연산 후 2-2로 이동
    12        color[p[x]] <-BLACK       >> CASE 2-2   // x의 부모 노드 RED -> BLACK
    13        color[p[p[x]]] <- RED     >> CASE 2-2   // 조부모 BLACK -> RED
    14        RIGHT-ROTATE(T, p[p[x]])  >> CASE 2-2   // 조부모를 중심으로 RIGHT-ROTATE 수행
    15    else(same as then clause with "right" and "left" exchanged) // CASE 3, 4-1, 4-2는 대칭적으로 똑같이 동작
    16 color[root[T]] <- BLACK // CASE 2-2, 4-2에서 문제를 해결하고 while문 탈출, CASE1, 3을 반복하다 루트 노드까지 올라간 후 while문이 종료된다면 RED이기 때문에 마지막 루트 노드를 BLACK
 ```

### INSERT의 시간복잡도
  - BST에서의 INSERT: `O(log n)`
  - RB-INSERT-FIXUP
    - Case 1, 3의 경우 x가 2레벨 상승
    - Case 2-1, 2-2, 4-1, 4-2에 해당할 경우 O(1)
    - 트리의 높이에 비례하는 시간복잡도를 가짐
  - INSERT의 시간복잡도는 `O(log n)`

### RB-INSERT-FIXUP 처리 흐름
  1. RED - RED 문제 발생
  2. Case 1에 해당할 경우 Case 1 수행, 이 경우 추가적인 연산  1, 2-1, 2-2에 해당하는 연산 필요
  3. Case 2-1에 해당하는 경우 2-1을 수행한 후 2-2 연산 진행
  4. Case 2-2에 해당하는 경우 2-2를 수행한 후 종료

## 삭제(Delete)
  - 보통의 BST처럼 Delete
  - 실제로 삭제된 노드 y가 RED 였으면 종료
  - y가 black이었을 경우 RB-DELETE-FIXUP 호출

### pseudo code
```java
    RB-DELETE(T, z)
    01 if left[z] = nil[T] or right[z] = nil[T]  // 삭제할 노드 자식이 없다면
    02   then y <- z                             // y에 z 저장
    03 else y <- TREE-SUCCESSOR(z)               // 자식이 있다면 z의 Successor을 찾아 y에 저장. BST에서 Successor 찾는 과정과 동일
    04 if left[y] != nil[T]                      // y의 왼쪽자식이 널이 아니라면 (1-3을 통해 y는 자식이 하나 이거나 없는 상태)
    05   then x <- left[y]                       // y의 왼쪽 자식을 x로
    06 else x <- right[y]                        // 그렇지 않다면, y의 오른쪽 자식을 x로 저장
    07 p[x] <- p[y]                              // y의 부모를 x의 부모로 설정
    08 if p[y] = nil[T]                          // y의 부모가 NULL이라면
    09   then root[T] <- x                       // x를 트리의 root로 설정
    10 else if y = left[p[y]]                    // y의 부모노드가 NULL이 아니고, y가 y의 부모의 왼쪽 자식 노드라면
    11   then right[p[y]] <- x                   // 저장한 x를 y의 부모의 왼쪽 자식노드로 설정
    12 else right[p[y]]                          // y가 y의 부모의 오른쪽 자식노드라면, 저장된 x를 부모노드의 오른쪽 자식으로 설정(여기까지가 실제로 노드를 삭제하는 작업)
    13 if y != z                                 // 삭제하는 노드 대신 Successor를 삭제한 경우 y != z, y노드의 데이터를 카피하는 작업 필요
    14   then key[z] <- key[y]                   // z에 y 데이터를 이전
    15     copy y's satellite data into z        // 14-15 y의 데이터를 z노드로 copy하는 작업
    16 if color[y] = BLACK                       // 삭제한 노드 y가 BLACK인 경우
    17   then RB-DELETE-FIXUP(T, x)              // 문제를 해결하기 위해 RB-DELETE-FIXUP(T, x)를 통해 규칙을 맞추기 위한 작업 수행. y의 자식인 x를 넘겨서 정렬
    18 return y                                  // 삭제된 노드 y 반환
```
  - **삭제한 노드가 BLACK인 경우 (Line 16)**
      - 삭제된 노드가 루트노드인데, 그 자식인 레드노드가 올라와서 루트가 된 경우
      - 중간의 black노드가 삭제되어서 RED-RED 위반이 생긴 경우
      - 트리를 따라 내려가면서 black노드의 개수가 일치하지 않는 경우가 생길 수 있음

### 조정 RB-DELETE-FIXUP(T, x) 
  - x가 NIL 노드일 수도 있다. 그리고 x가 RED인 경우 쉽게 해결 가능
  - 실제로 DELETE에서 문제가 되는 것은 x가 BLACK인 경우

**위반 될 수 있는 규칙**

- 각 노드는 RED 또는 BLACK
  - 문제 사항 없음
- 루트 노드는 BLACK
  - y가 루트였고, x가 RED인 경우 위반
- 모든 리프 노드(NIL 노드)는 BLACK
  - 문제 사항 없음
- RED 노드의 자식 노드들은 전부 BLACK(RED 노드는 연속으로 등장 불가)
  - p[y]와 x가 모두 RED인 경우 위반
  - x가 red인 경우 red를 black으로 바꾸어 주면 됨
- 모든 노드에 대해 그 노드로 부터 자손인 리프 노드(NIL 노드)에 이르는 모든 경로에는 동일한 개수의 BLACK 노드가 존재
  - 원래 y를 포함했던 모든 경로는 black노드가 하나 부족
    - 노드 x에 'extra black'을 부여하여 임시로 조건5 만족시킨다. 이는 색을 두개 가지게 하는 임시 방법
    - 노드 x는 'double black' 또는 'red & black'이 되는데 해당 노드를 black노드로 바꾸는 것이 해결해야할 문제

**문제 해결 방법**
  
  - Extra black을 순차적으로 트리의 위쪽으로 올려보냄
    - x의 부모가 double black이 되는 방식
  - x가 red & black 상태가 되면 black 노드로 바꾸고 종료
  - x가 루트가 되는 순간까지 올라가면 extra black을 제거
 
**Loop Invariant(루프를 돌면서 변하지 않고 유지되는 조건)**
  
  - x는 루트가 아닌 double-black노드
  - w는 x의 형제노드
  - w는 NIL 노드가 될 수 없음
    - NIL 노드일 시 x의 부모에 대해 조건5 위반

### Case 정의
  - DELETE의 경우 8가지 Case로 분류할 수 있음
    - Case 2의 상황을 p[x]가 RED, BLACK 두 가지로 나누어 다룰 경우 10가지 Case로 분류 가능
  - INSERT와 마찬가지로 1, 2, 3, 4와 5, 6, 7, 8은 대칭
  - Case 1, 2, 3, 4: x가 부모의 왼쪽 자식 노드인 경우
    - x는 double black 노드이거나, NIL 노드 일 수도 있음
    - x의 형제 노드인 노드 w는 반드시 존재하고, NIL일 수 없음
    - x는 자신의 부모의 왼쪽 자식
  - Case 5, 6, 7, 8: x가 부모의 오른쪽 자식노드인 경우
  
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-DelCase.png" width="600">
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-DelCase5.jpeg" width="600">

  - **Case 1: x의 형제노드 w가 RED인 경우**
    - Case 1,2,3,4의 공통 조건에 해당
    - 자식 노드가 NIL일 수 없고, BLACK 노드
    - 문제를 해결하기 위해 w를 BLACK으로 p[x]를 RED로 변경
    - p[x]에 대해 left-rotation을 수행. 현재 x는 여전히 double-black 노드
    - x의 새로운 형제 노드는 원래 w의 자식 노드
    - 따라서 새로운 w노드는 black 노드. 이 경우 Case 2, 3, 4로 넘어감
    - Case 1의 경우 x의 부모 노드에 대해 left-rotation을 수행하면, 새로운 w노드가 red가 아닌 black이 되기에 Case 2, 3, 4로 넘어감
   
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-DelCase1.png" width="700">
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-DelCase1.jpeg" width="600">

  - **Case 2: w는 BLACK, w의 자식들도 BLACK인 경우**
    - 해당 Case의 문제는 p[x]의 부모 노드가 RED인 경우, BLACK인 경우 두 Case로 분류하여 다루기도 함
    - Case 2, 3, 4는 x의 형제노드 w가 BLACK인 경우, w의 자식들도 모두 BLACK인 경우가 Case 2
    - x와 w가 모두 BLACK이므로 부모인 B노드는 RED일수도 있고, BLACK 일수도 있음
    - 현재 x는 double black 노드이고, w는 black 노드
    - 이 상황에서 x와 w로부터 black을 하나씩 뺏어서 부모노드에 전달
    - 결과적으로 x는 extra black이 사라져 black 노드, w는 black을 뺏겨 red 노드가 됨
    - 다음으로 p[x]에게 extra black을 전달
      - 트리 위에서 부터 내려오면서 유지하던 BLACK 노드의 개수를 유지하기 위함
    - 만약 p[x]가 RED였다면, red & black노드가 되어 BLACK노드로 변환하여 종료
    - p[x]가 BLACK이었다면 p[x]를 새로운 x로 설정하여 계속 진행
    - 만약 Case 1에서 Case 2에 도달한 경우면 p[x]는 RED였기에 새로운 x는 red & black이 되어 종료
    - Case 2로 바로온 경우 p[x]가 BLACK이었다면, p[x]가 double black이 되어 반복해서 문제를 해야할 수 있음
      - 다만 extra-black이 한 level 올라감
     
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-DelCase2.png" width="700">
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-DelCase2-1.jpeg" width="600">
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-DelCase2-2.jpeg" width="600">

  - **Case 3: w는 BLACK, w의 왼쪽 자식이 RED**
    - w를 RED로, w의 왼쪽 자식 노드를 BLACK으로 변환
    - w에 대해 right-rotation을 수행
    - x의 새로운 형제 w는 오른쪽 자식이 RED
    - 해당 경우는 Case 4에 해당
   
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-DelCase3.png" width="700">
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-DelCase3.jpeg" width="600">

  - **Case 4: w는 BLACK, w의 오른쪽 자식이 RED**
    - w의 색을 p[x]의 색(unknown color)으로 변경
    - p[x]를 BLACK으로, w의 오른쪽 자식을 BLACK으로 변경
    - p[x]에 대해 left-rotation을 수행
    - x의 extra black을 제거하고 종료
    - double black 노드가 없어졌음에도 불구하고 기존 A노드를 지나는 블랙노드의 개수가 로테이션 전과 동일, 나머지 C와 E를 지나는 블랙노드의 개수도 기존과 동일하게 유지됨
   
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-DelCase4.png" width="700">
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-DelCase4.jpeg" width="600">

### pesudo code
  - 레드블랙트리에서 실제로 삭제한 노드는 y
  - 삭제한 노드 y의 자식인 x를 넘겨주면서 Delete Fixup
```java
RB-DELETE-FIXUP(T, x)
01 while x != root[T] and color[x] = BLACK
02   do if x = left[p[x]]
03        then w <- right[p[x]] 
04          if color[w] = RED
05            then color[w] <- BLACK                                  // Case1
06                 color[p[x]] <- RED                                 // Case1
07                 LEFT-ROTATE(T, p[x])                               // Case1
08                 w <- right[p[x]]                                   // Case1
09          if color[left[w]] = BLACK and color[right[w]] = BLACK
10            then color[w] <- RED                                    // Case2
11                 x <- p[x]                                          // Case2
12          else if color[right[w]] = BLACK 
13              then color[left[w]] <- BLACK                          // Case3
14                   color[w] <- RED                                  // Case3
15                   RIGHT-ROTATE(T, w)                               // Case3
16                   w <- right[p[x]]                                 // Case3
17            color[w] <- color[p[x]]                                 // Case4
18            color[p[x]] <- BLACK                                    // Case4
19            color[right[w]] <- BLACK                                // Case4
20            LEFT-ROTATE(T, p[x])                                    // Case4
21            x <- root[T]                                            // Case4
22        else (same as then clause with "right" and "left" exchanged)
23 color[x] <- BLACK
```

    01: x가 루트노드이거나, x가 레드노드라면 while문 탈출 후 x를 BLACK으로 만들고 종료
    02: 왼쪽 자식인 경우, 오른쪽 자식인 경우로 크게 둘로 나뉨. 해당 경우는 x가 부모의 왼쪽 자식인 경우 수행(Case 1, 2, 3, 4), 
        오른쪽 자식인 경우 대칭적으로 수행(Case 5, 6, 7, 8)
    03: 노드 x의 형제 노드인 w를 저장
    04: 형제 노드 w가 RED인 경우 Case1
    05: w노드를 BLACK으로 만든다  
    06: p[x]노드를 RED로 만든다
    07: p[x]를 기준으로 LEFT-ROTATE
    08: 새로운 w는 p[x]의 right 이때, 새로운 노드 w는 BLACK이므로 다시 while문으로 들어왔을 때, Case 2, 3, 4로 이동
    09: Case 2, 3, 4를 구분. w의 왼쪽, 오른쪽 자식 노드가 둘 다 BALCK인 경우 Case 2
    10: w와 x에서 black을 하나씩 차출하여 부모 노드에게 전달하는 과정에서 w가 RED가 되고
    11: p[x]를 새로운 x로 설정. p[x]가 RED였다면 while을 돌지 않고 x를 RED로 만든 후 종료, p[x]가 BLACK이었다면 x를 p[x]로 두고 
        double-black 노드가 된 x를 다시 반복해서 처리
    12: w의 오른쪽 자식이 BLACK이고, 왼쪽 자식이 RED인 Case 3
    13: RIGHT-ROTATE의 대상인 노드 색 변경, w의 왼쪽 자식 노드 BLACK
    14: RIGHT-ROTATE의 대상인 노드 색 변경, w를 RED
    15: w를 기준으로 RIGHT-ROTATE
    16: w는 p[x]의 새로운 오른쪽 자식 노드가 되며 색이 RED가 되어 Case 4로 이동
    17: LEFT-ROTATE의 대상인 노드 색 변경, w를 p[x]의 색으로 변경
    18: LEFT-ROTATE의 대상인 노드 색 변경, p[x]의 색을 BLACK으로 변경
    19: w의 오른쪽 자식 노드 색을 BLACK으로 변경
    20: p[x]를 기준으로 LEFT-ROTATE
    21: 포인트 변수 x를 root[T]로 변경하여 Case 4가 종료되면 while문 종료(실제 트리에는 변화 없음, 트리의 루트의 변화도 없음)
    22: Case 5, 6, 7, 8을 대칭적으로 처리 (x가 p[x]의 오른쪽 자식인 경우)
    23: 트리의 루트 색을 BLACK으로 변경


### RB-DELETE-FIXUP의 Case 흐름
  - 전체 Case는 1 - 8의 경우지만 1, 2, 3, 4와 5, 6, 7, 8은 대칭적인 관계 
  - 처음부터 Case 4의 경우에 해당하면 left-rotation과 extra-black노드를 뺏는 것으로 Case 종료
  - Case 3인 경우 right-rotation으로 Case 3를 해결하고 Case 4로 진행
  - Case 1인 경우 Case 1을 해결하고 Case 2, 3, 4 중 하나로 진행
  - Case 2인 경우 Case 1에서 넘어온 것이면 Case2를 해결하고 종료되지만 바로 Case 2로 진행된 경우 반복적으로 문제를 해결해야할 수 있음
  - Case 2가 만복되는 동안 extra-black 노드는 계속해서 트리의 위로 이동, 이 상황에서 Case 1, 3, 4로 이동하게 되면 흐름에 따라 2step 이내에 종료
  - Case 5, 6, 7, 8로 넘어가 Case 2와 대칭인 Case 6의 경우와 순환할 수도 있고, Case 5, 7, 8로 이동하여 종료될 수도 있음

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RBT-DelFlow.png" width="600">


### DELETE의 시간복잡도
  - BST에서의 DELETE: `O(log n)`
  - RB-DELETE-FIXUP: `O(log n)`
    - 가장 최악의 경우인 Case 2와 Case 6가 반복되는 경우에도 최대 트리의 높이만큼 실행
  - DELETE와 FIXUP을 합쳐도 `O(log n)`

> ⬆️:[Top](#Red-Black-Tree)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#1-data-structure)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [01. Red-Black Tree 개요](https://github.com/namjunemy/TIL/blob/master/Algorithm/red_black_tree_01.md)
> - [02. Red-Black Tree insert fix-up](https://github.com/namjunemy/TIL/blob/master/Algorithm/red_black_tree_02.md)
> - [03. Red-Black Tree delete, fix-up](https://github.com/namjunemy/TIL/blob/master/Algorithm/red_black_tree_03.md)
