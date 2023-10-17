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
3. 간선의 갯수가 V-1개가 될 때까지 모든 간선에 대해 2번 과정을 반복한다.

### 예시 

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
