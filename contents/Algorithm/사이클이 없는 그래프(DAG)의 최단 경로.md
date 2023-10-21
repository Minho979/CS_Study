# 사이클이 없는 그래프(DAG)의 최단 경로
## 개념
- 그래프의 한 정점에서 다른 정점까지의 최단 경로를 구하는 알고리즘
- DAG에서의 최단경로는 선형시간에 간단하게 구할 수 있다.

## 동작 과정
1. 위상 정렬을 통해서 방문 순서대로 정점을 정렬
2. 각 정점마다 Relaxtion을 통해 해당 정점과 연결되어 있는 정점들 중 최단거리를 찾는다.

### 예시 

## 시간 복잡도
- 정점 수: V, 간선 수: E
- 위상 정렬을 수행하는 시간: $𝛩(V+E)$
- 모든 정점을 초기화하는 시간: $𝛩(V)$
- 각 정점에 대한 Relaxtion을 수행하는 시간 $𝛩(|E|)$
- 최종적으로 위의 연산을 모두 합친  $𝛩(V+E)$

> ⬆️:[Top](#사이클이-없는-그래프DAG의-최단-경로)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EC%B5%9C%EB%8B%A8%20%EA%B2%BD%EB%A1%9C(Shortest%20path)%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md#%EB%8B%A8%EC%9D%BC-%EC%8B%9C%EC%9E%91%EC%A0%90-%EC%B5%9C%EB%8B%A8-%EA%B2%BD%EB%A1%9C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[알고리즘 정리] DAG에서 최단경로를 찾는 법](https://jeonyeohun.tistory.com/99)
