# 최단 경로(Shortest path) 알고리즘
## 개념
- 두 정점 사이의 경로 중 간선의 가중치 합이 최소인 경로
- 간선의 가중치 합이 음인 사이클이 있으면 문제가 정의되지 않는다.

## 조건
- 간선 가중치가 있는 유향 그래프(directed weighted graph)이어야 한다.
- 그래프가 무향 그래프라면 양쪽으로 유향 간선이 있는 유향 그래프로 생각할 수 있다.
  - 즉, 무향 간선(i, j)를 유향 간선 <i, j>와 <j, i>로 간주한다.

## 여러 종류의 최단 경로 알고리즘
### 단일 시작점 최단 경로 알고리즘
- 하나의 시작 정점으로부터 각 정점에 이르는 최단 경로를 구하는 알고리즘
- n개의 결과가 나온다.
- **[다익스트라(Dijkstra) 알고리즘](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EB%8B%A4%EC%9D%B5%EC%8A%A4%ED%8A%B8%EB%9D%BC(Dijkstra)%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md)**
  - 음의 가중치를 허용하지 않는 최단 경로
- **[벨만-포드(Bellman-Ford) 알고리즘](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EB%B2%A8%EB%A7%8C-%ED%8F%AC%EB%93%9C(Bellman-Ford)%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md)**
  - 음의 가중치를 허용하는 최단 경로
- **[사이클이 없는 그래프(DAG)의 최단 경로](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EC%82%AC%EC%9D%B4%ED%81%B4%EC%9D%B4%20%EC%97%86%EB%8A%94%20%EA%B7%B8%EB%9E%98%ED%94%84(DAG)%EC%9D%98%20%EC%B5%9C%EB%8B%A8%20%EA%B2%BD%EB%A1%9C.md)**

### 모든 쌍 최단 경로 알고리즘
- 모든 정점 쌍 사이의 최단 경로를 모두 구하는 알고리즘
- n*n개의 결과가 나온다.
- **[플로이드-워샬(Floyd-Warshall) 알고리즘](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%ED%94%8C%EB%A1%9C%EC%9D%B4%EB%93%9C-%EC%9B%8C%EC%83%AC(Floyd-Warshall)%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md)**

> ⬆️:[Top](#최단-경로Shortest-path-알고리즘)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
