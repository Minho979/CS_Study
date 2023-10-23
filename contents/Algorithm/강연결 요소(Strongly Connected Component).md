# 강연결 요소(Strongly Connected Component)
## 개념
- 유향 그래프 G의 모든 정점쌍에 대해서 양방향으로 경로가 존재하는 경우 강하게 연결되었다(Strongly Connected)고 한다.
- 강하게 연결된 부분 그래프(subgraph)를 강연결 요소(SCC: Strongly Connected Component)라고 한다.
- 그래프 전체는 강한 연결이 아니지만 부분 그래프에서 여러 개의 강연결 그래프가 있을 수 있다
- 같은 SCC 내에 속해 있는 두 정점에 대해 경로가 항상 있기에 사이클이 존재한다.
- 서로 다른 SCC에 속하는 두 정점은 서로 양방향으로 연결될 수 없어 SCC 간에는 사이클이 존재할 수 없다.

## 동작 과정
1. 그래프 G에 대해 DFS로 각 정점의 완료 시간대로 스택에 기록한다.
2. G의 모든 간선들의 방향을 반대로 뒤집어 준다.
   - 뒤집힌 그래프를 G'이라고 가정
3. G' 그래프에 DFS를 수행한다. 이때, 1번 과정에서 구한 완료 시간이 가장 큰 늦은 정점을 루트 노드로 삼아아 늦은 정점 순으로 진행한다. (LIFO)

   3-1. DFS를 수행하며 더이상 상위노드로 이동할 수 없을 때, SCC를 발견하고 기록하는 과정을 스택이 빌때까지 반복한다.

### 예시

## 시간 복잡도
- 모든 정점을 탐색하고 간선의 개수만큼 추가 탐색하므로 $O(|V|+|E|)$ 
   
> ⬆️:[Top](#강연결-요소Strong-Connected-Component)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
