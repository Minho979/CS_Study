# 벨만-포드(Bellman-Ford) 알고리즘
## 개념
- 그래프의 한 정점에서 다른 정점까지의 최단 경로를 구하는 알고리즘
- `정점 수 - 1`번의 매 단계마다 모든 간선을 전부 확인하면서 모든 노드간의 최단 거리를 구한다.
- 간선 가중치의 범위가 임의의 실수로 음의 가중치인 경우에도 사용이 가능하다.

## 동작 과정
1. 출발 노드를 설정
2. '최단 거리 테이블' 초기화
3. 다음 과정을 `정점 수 - 1`번 반복
   
    3-1. 모든 간선 E개를 하나씩 확인

    3-2. 각 간선을 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신

4. 음수 간선 순환이 발생하는지 3번 과정을 한번 더 수행하여 확인
    - 이때 최단 거리 테이블이 갱신된다면 음수 간선 순환이 존재

### 예시

## 시간 복잡도
- 정점 수: V. 간선 수: E 
- `정점 수 - 1`개 만큼 사이클을 돌고 각 사이클 마다 간선을 확인하므로 $O(|V-1||E|)$ 
- $O(|V||E|)$


> ⬆️:[Top](#벨만-포드Bellman-Ford-알고리즘)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EC%B5%9C%EB%8B%A8%20%EA%B2%BD%EB%A1%9C(Shortest%20path)%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md#%EB%8B%A8%EC%9D%BC-%EC%8B%9C%EC%9E%91%EC%A0%90-%EC%B5%9C%EB%8B%A8-%EA%B2%BD%EB%A1%9C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
