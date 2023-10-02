# Graph
## Graph의 개념

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/Graph.png" width="500" height="310">

  - 단순히 정점(V, vertex)와 그 노드를 연결하는 간선(E, edge)를 하나로 모아 놓은 자료구조
    - 연결되어 있는 객체 간의 관계를 표현할 수 있음
    - 정점은 대상을 나타내고, 간선은 대상들 간의 관계를 나타냄
    - 그래프는 여러 개의 고립된 부분 그래프(Isolated Subgraphs)로 구성될 수 있음
    - 원소들 간의 n:n관계를 표현할 수 있음
    - 예) 지도, 지하철 노선도의 최단 경로,회로의 소자들, 도로(교차점과 일방통행길), 선수 과목 등

## Graph의 종류
### 무방향 그래프(undirected graph)

<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/undirectedGraph.png" width="500">
    
- 간선에 방향이 없는 그래프
- (v1, v2)와 (v2, v1)은 동일한 간선

### 방향 그래프(directed graph)

![digraph](https://github.com/Minho979/CS_Study/blob/main/contents/images/digraph.png)
    
- 간선에 방향이 있는 그래프
- 다이그래프(digraph)라고도 부름
- <v1, v2>와 <v2, v1>은 다른 간선
  - v1(tail) -> v2(head)로 가는 간선을 <v1, v2>로 표현

### 완전 그래프(complete graph)

![completeGraph](https://github.com/Minho979/CS_Study/blob/main/contents/images/completeGraph.png)

- 각 정점에서 다른 모든 정점으로의 간선이 존재하는 그래프
  - 주어진 정점 수에 대해 간선 수가 최대

### 가중 그래프(weighted graph)

![weightedGraph](https://github.com/Minho979/CS_Study/blob/main/contents/images/weightedGraph.png)

- 간선에 가중치(weight)가 주어진 그래프
  - 가중치는 두 정점 사이의 비용이나 거리, 시간 등을 의미하는 값
- 가중치를 이용하여 최소 비용, 최대 비용 등을 계산하는데 이용 가능

## 그래프 순회(Graph Traversal)
- 그래프 탐색(Graph Search)라고도 함
- 하나의 정점에서 시작하여 그래프의 모든 정점을 한번씩 방문
- 깊이 우선 탐색(Depth First Search: DFS), 너비 우선 탐색(Breadth First Search: BFS)로 구분
### DFS

<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/DFS.png" width="300">
<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/DFS1.png" width="500">
      
- 한 방향으로 가장 먼(깊은) 정점을 방문하는 것을 반복하는 순회 방식
  1. 시작 정점에서 한 방향으로 가장 먼 경로까지 깊이 탐색
  2. 더이상 진출이 불가능할 시 갈림길 간선이 있는 정점으로 복귀
  3. 다른 방향의 간선으로 탐색을 지속
  4. b, c를 반복하여 시작 정점으로 복귀
- 스택을 이용하여 구현하거나 재귀 알고리즘을 이용하여 구현

### BFS

<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BFS.png" width="300">
<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BFS1.png" width="500">
      
- 가장 가까운 정점들을 방문하고 멀리있는 정점은 가장 나중에 방문하는 순회 방식
  1. 시작 정점에서 인접한 정점들을 방문
  2. 방문했던 정점을 기준으로 다시 인접한 정점들을 방문
- 차례대로 탐색을 진행하므로 선입선출 구조의 큐를 이용하여 구현
     
## Graph의 특징
  - 네트워크 모델
  - 2개 이상의 경로가 가능
    - 정점들 사이에 무방향/방향에서 양방향 경로를 가질 수 있음
  - self-loop뿐 아니라 loop/circuit 모두 가능
  - 루트 정점(노드)라는 개념이 없음
  - 부모-자식 관계라는 개념이 없음
  - 순회는 DFS(Depth First Search)나 BFS(Breadth First Search)로 이루어짐
  - 그래프는 순환(Cyclic) 혹은 비순환(Acyclic)
  - 그래프는 크게 방향 그래프와 무방향 그래프가 있음
  - 간선의 유무는 그래프에 따라 다름

> ⬆️:[Top](#1-DataStructure)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#1-data-structure)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [이지영. 지바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[자료구조] 그래프(Graph)란](https://gmlwjd9405.github.io/2018/08/13/data-structure-graph.html)
