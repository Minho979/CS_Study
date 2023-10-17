# Kruskal 알고리즘
최소 신장 트리(Minimum Spanning Tree) 구현에 사용되는 알고리즘
- [신장트리란?](https://github.com/Minho979/CS_Study/blob/main/contents/Data%20Structure/Graph.md#%EC%8B%A0%EC%9E%A5-%ED%8A%B8%EB%A6%ACspanning-tree%EC%99%80-%EC%B5%9C%EC%86%8C%EB%B9%84%EC%9A%A9-%EC%8B%A0%EC%9E%A5-%ED%8A%B8%EB%A6%AC)

## 개념 
- 그래프 G=(V, E)의 최소 신장 트리를 이루는 간선 집합 T에 공집합으로 시작하여 사이클 없이 모든 정점이 최소 비용으로 연결될때(T=V-1)까지 간선을 T에 추가하는 방법

## 동작 과정
1. 간선 정보를 가중치에 따라 오름차순으로 정렬
2. 간선을 하나씩 확인하며 현재 간선이 사이클을 발생시키는지 체크한다.

   2-1. 사이클이 발생하면 최소 신장 트리에 포함하지 않는다.

   2-2. 사이클이 발생하지 않으면 최소 신장 트리에 포함한다.
4. 간선의 갯수가 V-1개가 될 때까지 모든 간선에 대해 2번 과정을 반복한다.

### 예시 
- 사용된 무방향 그래프
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Kruskal-Graph.png' width='500'>

0. 그래프의 간선 정보를 가중치에 따라 오름차순 정렬

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Kruskal-initial-state.png' width='700'>
1. `(from, to, cost) = (1, 7, 12)`

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Kruskal-step1.png' width='700'>
   
   - `find(1) = 1`, `find(7) = 7`으로 부모 노드가 서로 다르므로 MST에 추가해도 사이클이 발생하지 않음
   - `union(1, 7)`로 같은 MST로 묶어줌
     - 7의 부모를 1로 변경
2. `(from, to, cost) = (4, 7, 13)`

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Kruskal-step2.png' width='700'>

   - `find(4) = 4`, `find(7) = 1`으로 부모 노드가 서로 다르므로 MST에 추가해도 사이클이 발생하지 않음
   - `union(4, 7)`로 같은 MST로 묶어줌
     - 4의 부모를 1로 변경
3. `(from, to, cost) = (1, 5, 17)`

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Kruskal-step3.png' width='700'>
   
   - `find(1) = 1`, `find(5) = 5`으로 부모 노드가 서로 다르므로 MST에 추가해도 사이클이 발생하지 않음
   - `union(1, 5)`로 같은 MST로 묶어줌
     - 5의 부모를 1로 변경
4. `(from, to, cost) = (3, 5, 20)`

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Kruskal-step4.png' width='700'>
   
   - `find(3) = 3`, `find(5) = 1`으로 부모 노드가 서로 다르므로 MST에 추가해도 사이클이 발생하지 않음
   - `union(3, 5)`로 같은 MST로 묶어줌
     - 3의 부모를 1로 변경
5. `(from, to, cost) = (2, 4, 24)`

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Kruskal-step5.png' width='700'>
   
   - `find(2) = 2`, `find(4) = 1`으로 부모 노드가 서로 다르므로 MST에 추가해도 사이클이 발생하지 않음
   - `union(2, 4)`로 같은 MST로 묶어줌
     - 2의 부모를 1로 변경   
6. `(from, to, cost) = (1, 4, 28)`

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Kruskal-step6.png' width='700'>

   - `find(1) = 1`, `find(4) = 1`으로 부모 노드가 서로 같으므로 MST에 추가할 경우 사이클이 발생
   - MST에 추가하지 않고 넘어감
7. `(from, to, cost) = (3, 6, 37)`

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Kruskal-step7.png' width='700'>

   - `find(3) = 1`, `find(6) = 6`으로 부모 노드가 서로 다르므로 MST에 추가해도 사이클이 발생하지 않음
   - `union(3, 6)`로 같은 MST로 묶어줌
     - 6의 부모를 1로 변경 
8. `(from, to, cost) = (5, 6, 45), (2, 5, 62), (1, 2, 67), (5, 7, 73)`

    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Kruskal-step8-final.png' width='700'>

   - 사이클 테이블의 모든 값이 1로 같은 부모 노드를 가지고 있음
   - 따라서 남은 간선 4개는 모두 MST에 추가하지 않고 넘어감

## 시간 복잡도
- Union-Find 알고리즘을 이용하면 Kruskal 알고리즘은 간선을 정렬하는 시간에 좌우됨
- 간선 e개를 효율적인 알고리즘으로 정렬한다면 시간 복잡도는 $O(Elog E)$가 된다
- 간선의 수는 최대 $V^2$개가 될 수 있으므로 $O(log E) = O(log V^2) = O(2log V) = O(log V)$가 성립한다.
- 최종적으로 $O(Elog V)$의 시간 복잡도를 가진다.

## Kruskal vs Prim 알고리즘
### Kruskal 알고리즘
- 간선 중심의 알고리즘
- 트리를 이용하여 집합으로 구현
  - 랭크를 이용한 Union, 경로 압축을 이용한 Find-Set
- 시작점을 정하지 않고 최소 비용의 간선을 차례로 대입하면서 트리를 구성
  - 사이클 형성 여부 확인 절차 필요
- 간선이 적은 경우가 유리
- $O(|E|log |V|)$의 시간 복잡도를 지님

### Prim 알고리즘
- 정점 중심의 알고리즘
- 우선순위 큐를 이용한 최소 힙으로 구현
- 시작정을 정하고, 시작점에서 가까운 정점을 선택하여 트리를 구성
  - 구성 과정에서 사이클 형성이 없음
- 간선의 개수가 많은 경우 유리
- $O(|E|log |V|)$의 시간 복잡도를 지님

## 구현 

> ⬆️:[Top](#Kruskal-알고리즘)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [18. 크루스칼 알고리즘(Kruskal Algorithm)](https://blog.naver.com/ndb796/221230994142)
> - [[알고리즘/Java] 크루스칼(Kruskal) 알고리즘](https://velog.io/@suk13574/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98Java-%ED%81%AC%EB%A3%A8%EC%8A%A4%EC%B9%BCKruskal-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
