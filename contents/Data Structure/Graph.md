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

## 그래프 용어 정리
### 인접(adjacent), 부속(incident)
- 두 정점 $v_i$와 $v_j$ 사이에 간선 ($v_i, v_j$)가 존재하면 와 $v_j$는 인접하다(adjacent)
- ($v_i, v_j$)는  $v_i$와 $v_j$에 부속되어 있다(indicent)

### 차수(degree)
- 정점의 차수 = 정점에 부속된(incident) 간선의 수
- 방향 그래프의 정점의 차수 = 진입차수(in-degree)  + 진출차수(out-degree)

### 경로(path)
- 그래프에서 한 정점에서 한 정점으로 간선을 따라 도달할 수 있는 길
- 정점 $v_i$에서 정점 $v_j$까지의 경로란 $v_i$에서 $v_j$에 이르기까지 간선으로 연결된 정점들을 순서대로 나열한 리스트
- 경로 길이(path length) : 경로를 구성하는 간선의 수
  - 경로 A-B-C의 길이 = 2

### 단순 경로(simple path)
- 모두 다른 정점들로 구성된 경로(단, 시작 정점과 마지막 정점은 동일해도 됨)
  - 시작과 마지막 정점이 아닌 경로 중간에 한 번 간 곳을 다시가면 단순 경로가 아님
- 사이클(cycle) : 시작 정점과 마지막 정점이 같은 단순 경로

### DAG(Directed Acyclic Graph)
- 사이클이 없는 방향 그래프

### 연결(connected)
- 정점 $v_i$에서 $v_j$까지 경로가 있으면 $v_i$와 $v_j$가 연결되었다고 함

### 연결 그래프(connected graph)
- 모든 쌍의 정점들 사이에 경로가 있는 그래프

### 부분 그래프(subgraph)
- 원래의 그래프에서 정점이나 간선의 일부를 취해 만든 그래프
- 그래프 G와 부분 그래프 G'의 관계 : $V(G')\subseteqq V(G), E(G') \subseteqq E(G)$
- 정점을 하나 제거할 경우 해당 정점에서 이어진 간선을 모두 제거해야 한다.

## 그래프의 구현
### 인접 행렬
### 개념
2차원 배열로 표현한 행렬에 두 정점의 인접 여부(간선의 존재 여부)를 저장
- n개의 정점을 가진 그래프: n*n 정방행렬
- 행렬의 행번호/열번호: 그래프의 정점
- 행렬 i행 j열 원소 값: 정점 i와 j가 인접한 경우 1, 아닌 경우 0
- 행렬에 표기시 행이 출발 정점이며 열이 도착 정점

### 무방향 그래프의 인접 행렬
- 간선 (i, j) 에 대해 두개의 행렬 원소(i행 j열, j행 i열)가 1
- i행의 합 = i열의 합 = 정점 i의 차수

### 방향 그래프의 인접 행렬
- 간선 <i, j> 에 대해 하나의 행렬 원소 (i행 j열)가 1
- i행의 합 = 정점 i의 out-degree
- i열의 합 = 정점 i의 in-degree

### 인접 행렬의 장점
- 배열의 장점들을 모두 가짐(검색 성능, 처리 속도, 관리 용이 등)
- 배열의 장점을 살려 간단하게 알고리즘을 구현 가능

### 인접 행렬의 단점
- 정점이 n개이면 간선 수와 상관 없이 n x n 개의 메모리를 사용
- 희소 그래프에 대한 인접 행렬은 희소 행렬이 되므로 메모리 낭비
- 희소 그래프인 경우 일부 연산은 불필요하게 오래 걸림(의미 없는 정보를 많이 포함하고 있음)
    - 희소 그래프: 정점수에 비해 간선수가 적은 그래프
    - 희소 그래프의 인접 행렬은 희소 행렬(sparse matrix)
- 인접 행렬 표현은 그래프 간선의 밀도가 높은 경우 적합한 방법

### 인접 리스트
### 개념
- 각 정점에 대해 인접한 정점들이 무엇인지 연결 리스트로 표현
  - 각 정점마다 하나의 연결 리스트를 둠
- 인접 리스트 예시
  - n개의 정점을 가지는 그래프의 경우
    - 연결 리스트가 n개와 연결 리스트의 첫번째 노드를 가리키는 변수가 n개 필요
    - 이 변수들을 배열(크기 n)로 구현

### 무방향 그래프의 인접 리스트
- 정점 n개, 간선 e개
- Node형 변수 배열의 크기 : n
- 전체 노드 개수 : 2e
- 정점 v에 대한 리스트의 노드 개수 = v의 degree
    
    리스트의 노드의 개수 = 리스트의 길이

### 방향 그래프의 인접 리스트
- 정점 n개, 간선 e개
- Node형 변수 배열의 크기 : n
- 전체 노드 개수 : e
- 정점 v에 대한 리스트의 노드 개수 = v의 out-degree
    
    정점  v의 degree를 구하는 시간은 정점 v의 차수에 비례

#### 인접 리스트에서의 희소 그래프
- n = 100, e = 4
- 노드형 변수 배열의 크기 = 100
    - 간선 수와 관계 없이 노드 수에 맞는 Ndoe형 변수 배열이 필요

### 인접 리스트의 장점
- 간선의 개수에 비례한 메모리 공간
- 희소 그래프에서의 탐색의 효율성

### 인접 리스트의 단점
- 노드의 연결 여부를 알고 싶을 때 인접 행렬보다 시간 복잡도가 높음 

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

## 신장 트리(spanning tree)와 최소비용 신장 트리
### 신장 트리(spanning tree)
### 개념
- n개의 정점으로 이루어진 무방향 연결 그래프의 subgraph 중에서, 정점은 n개 전부 포함하고, 간선은 n-1개만 포함하여 모든 정점들이 연결되는 subgraph
- 신장 트리는 최소 개수의 간선으로 그래프의 모든 정점들이 연결되도록 함
### 신장 트리의 종류
- 깊이 우선 신장 트리(depth first spanning tree)
    - 깊이 우선 탐색을 이용하여 생성된 신장 트리
- 너비 우선 신장 트리(breadth first sapnning tree)
    - 너비 우선 탐색을 이용하여 생성된 신장 트리

### 최소 비용 신장 트리(minimum cost spanning tree)
### 개념
- 무방향 가중 연결 그래프(undirected weighted connected graph)의 신장 트리 중, 간선 가중치 합이 최소인 신장 트리

### 최소 비용 신장 트리를 구하는 알고리즘
#### Kruskal 알고리즘 I
가중치가 높은 간선을 제거하면서 최소 비용 신장 트리를 만드는 알고리즘
- 수행과정
  1. 그래프 G의 모든 간선을 가중치에 따라 내림차순으로 정렬
  2. 그래프 G에 가중치가 가장 높은 간선을 고른다.
     
      이 간선을 제거해도 그래프가 분리되지 않으면 이 간선을 제거하고,
      이 간선을 제거하는 경우 그래프가 분리되면 이 간선을 그대로 두고 다음 간선으로 넘어간다

  3. 그래프에 n-1개의 간선만 남을 때까지 2를 반복한다

#### Kruskal 알고리즘 II
정점들은 그대로 두고 간선이 하나도 없는 상태에서 시작하여 가중치가 낮은 순서로 간선을 삽입하면서 최소 비용 신장 트리를 만드는 알고리즘 
- 수행과정
    1. 그래프 G의 모든 간선을 가중치에 따라 오름차순으로 정렬한다.
    2. 그래프 G에 가중치가 가장 작은 간선을 고른다.
        
        이 간선이 사이클을 형성하지 않으면 트리 간선 집합 T에 삽입하고, 사이클을 형성하면 버리고 가중치가 다음으로 작은 간선을 선택한다.
        
    3. T가 n-1개의 간선을 포함할 때까지 2를 반복한다.

#### Prim 알고리즘
하나의 정점에서 시작하여 모든 정점이 포함될 때까지 최소 비용 신장 트리를 확장해 나가는 알고리즘으로 간선을 정렬하는 과정이 없다.
- 수행과정
    1. 그래프 G에서 시작 정점을 선택하여 트리 정점 집합 T에 삽입한다.
    2. 트리 정점과 트리 밖 정점에 부속된 간선 중에서 가중치가 가장 작은 간선을 선택하여 트리를 확장한다.
        
        이 때 선택된 간선의 한쪽 끝인 트리 밖 정점을 T에 삽입한다.
        
    3. T가 n개의 정점을 포함할 때까지 2를 반복한다.

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

> ⬆️:[Top](#Graph)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#-Data-Structure)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [이지영. 지바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[자료구조] 그래프(Graph)란](https://gmlwjd9405.github.io/2018/08/13/data-structure-graph.html)
