# Prim 알고리즘
최소 신장 트리(Minimum Spanning Tree) 구현에 사용되는 알고리즘
- [신장트리란?](https://github.com/Minho979/CS_Study/blob/main/contents/Data%20Structure/Graph.md#%EC%8B%A0%EC%9E%A5-%ED%8A%B8%EB%A6%ACspanning-tree%EC%99%80-%EC%B5%9C%EC%86%8C%EB%B9%84%EC%9A%A9-%EC%8B%A0%EC%9E%A5-%ED%8A%B8%EB%A6%AC)

## 개념
- 그래프 G=(V, E)의 최소 신장 트리를 이루는 정점 집합 S를 공집합에서 시작하여 모든 정점을 포함할 때까지(S=V)까지 트리를 확장하는 기법
- 배열, 우선순위 큐를 이용한 최소 힙으로 구현이 가능
- 새로운 정점을 연결할 때마다 새로운 정점에서 갈 수 있는 아직 연결되지 않은 정점들에 대한 간선을 추가해야 함

## 동작 과정
- 초기 상태
  - 정점(노드)는 서로 연결되어 있지 않으며 부속된 간선의 가중치를 알고 있는 상황
1. 시작 정점을 정해 해당 정점을 가중치를 0으로하여 큐에 (정점, 가중치) 형식으로 삽입한다.
2. 큐에서 하나의 정점(v)을 꺼낸다.
3. v가 MST에 포함되어 있다면 2로 돌아가서 반복하고, 그렇지 않다면 진행한다.
4. v와 연결된 간선을 살펴본다. 정점 w를 방문하지 않았다면 w를 큐에 추가한다.

   간선(w, cost)는 정점 v와 정점 w사이에 cost의 가중치로 연결된 간선을 의미한다.

### 예시
0. 그래프의 초기 상태
   
   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/prim-Graph.png' width='500'>
   
   - v: 정점
   - w: 이어진 정점(방문 가능 정점)
   - Cost: 가중치
   - visit: Boolean 배열로 각 정점 방문 여부 체크
   - 우선순위 큐: (정점, 가중치) 형태로 저장되며 가중치를 기준으로 정렬(가중치가 적을 수록 우선순위가 높음)
   - 시작 정점이 1이기에 우선순위 큐에 (1, 0)이 삽입되어 있는 상황
     - 첫 정점은 가중치 0

1. 우선 순위 큐에서 값을 하나 꺼냄 (1, 0)

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/prim-step1.png' width='500'>
   
   - 아직 방문된적 없는 정점이므로 방문 체크
   - 정점 1을 MST에 삽입하고 정점 1과 연결된 간선들을 체크
   - 방문된적 없는 정점 3, 4, 2를 각각 가중치와 함께 큐에 삽입

2. 우선 순위 큐에서 값을 하나 꺼냄 (3, 3)

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/prim-step2.png' width='500'>

   - 아직 방문한적 없는 정점이므로 방문 체크
   - MST에 (3, 3) 삽입하고 정점 3과 연결된 간선들을 체크
   - 방문된적 없는 정점 2를 가중치와 함께 큐에 삽입
     - 이미 MST에 삽입된 정점 1은 제외

3. 우선 순위 큐에서 값을 하나 꺼냄 (4, 8)

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/prim-step3.png' width='500'>

   - 아직 방문한적 없는 정점이므로 방문 체크
   - MST에 (4, 8) 삽입하고 정점 4와 연결된 간선들을 체크
   - 방문된적 없는 정점 5를 가중치와 함께 큐에 삽입

4. 우선 순위 큐에서 값을 하나 꺼냄 (5, 9)

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/prim-step4.png' width='500'>

   - 아직 방문한적 없는 정점이므로 방문 체크
   - MST에 (5, 9) 삽입하고 정점 5와 연결된 간선들을 체크
   - 방문된적 없는 정점 2를 가중치와 함께 큐에 삽입
  
5. 우선 순위 큐에서 값을 하나 꺼냄 (2, 10)

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/prim-step5.png' width='500'>

   - 아직 방문한적 없는 정점이므로 방문 체크
   - 정점 2와 연결된 간선들을 체크
   - 모든 간선이 MST에 포함된 정점과 연결되어 넘어감
    
6. 우선 순위 큐에서 값을 하나 꺼냄 (2, 13)

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/prim-step6.png' width='500'>

   - 이미 방문한 정점이므로 넘어감
    
7. 우선 순위 큐에서 값을 하나 꺼냄 (2, 14)

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/prim-step7.png' width='500'>

    - 이미 방문한 정점이므로 넘어감
  
8. 우선 순위 큐가 비었으므로 MST 구성 종료

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/prim-result.png' width='500'>

   - 최종 총 가중치 30 

## 시간 복잡도
- 배열로 구현한 경우: $O(V^2)$
  - 최소 간선을 갖는 정점 탐색을 매번 정점마다 수행하여 $O(|V|^2)$
- 우선순위 큐를 이용한 최소힙으로 구현하는 경우: $O(Elog V)$
  - 모든 노드에 대해 탐색을 진행하여 노드의 최소 간선을 찾는 시간: $O(Vlog V)$
  - 각 노드의 인접 간선을 찾는 시간(= 모든 노드의 차수): $O(E)$
  - 각 간선을 힙에 넣는 과정: $O(log V)$
  - 우선순위 큐 구성에 소요되는 시간: $O(Elog V)$
  - $O(Vlog V + Elog V)$이지만 E가 일반적으로 V보다 크기에 $O(Elog V)$

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

## 구현 코드
``` java 
```

> ⬆️:[Top](#Prim-알고리즘)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[알고리즘/Java] 프림(Prim) 알고리즘](https://velog.io/@suk13574/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98Java-%ED%94%84%EB%A6%BCPrim-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
