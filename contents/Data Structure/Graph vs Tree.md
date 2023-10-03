# Graph와 Tree의 차이점
||그래프|트리|
|:-----:|---|---|
|정의|노드(node)와 노드를 연결하는 간선(edge)를 하나로 모아 놓은 자료 구조|그래프의 한 종류 <br> DAG(Directed Acyclic Graph, 방향성이 있는 비순환 그래프)의 한 종류|
|방향성|방향그래프(Directed), <br> 무방향 그래프(Undirected) 모두 존재|방향 그래프(Directed Graph)|
|사이클|사이클(Cylce) 가능, 자체 간선(self-loop)가능, 순환 그래프(Cyclic), 비순환 그래프(Acyclic) 모두 존재|사이클(Cycle) 불가능, 자체 간선(self-loop)도 불가능, 비순환 그래프(Acyclic Graph)|
|루트 노드|루트 노드의 개념이 없음|한 개의 루트 노드만이 존재, 모든 자식 노드는 한 개의 부모 노드만을 가짐|
|부모-자식|부모-자식의 개념이 없음|부모-자식 관계 top-bottom 또는 bottom-top으로 이루어짐|
|모델|네트워크 모델|계층 모델|
|순회|DFS, BFS|DFS, BFS 속의 Pre-,In-,Post-order|
|간선의 수|그래프에 따라 간선의 수가 다름, 간선이 없을 수도 있음|노드가 N인 트리는 항상 N-1개의 간선을 가짐|
|경로|-|임의의 두 노드 간의 경로는 유일|
|예시 및 종류|지도, 지하철 노선도의 최단 경로, 전기 회로의 소자들, 도로(교차점과 일반 통행길), 선수과목|이진 트리, 이진 탐색 트리, 균형 트리(AVL 트리, Red-Black 트리), 이진 힙(최대힙, 최소힙)등|

> ⬆️:[Top](#Graph와-Tree의-차이점)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#-Data-Structure)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [이지영. 지바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
