# 플로이드-워샬(Floyd-Warshall) 알고리즘
## 개념
- 모든 정점들간의 상호 최단 경로를 구하는 알고리즘
- 거쳐가는 노드를 기준으로 알고리즘을 수행
- 동적 프로그래밍 기법을 사용하는 알고리즘
- 인접 행렬을 이용하여 정점 간의 최소 비용을 계산

## 주의 사항
- 현재 노드가 포함된 행과 열은 업데이트 하지 않는다
  - 1번 노드가 선택된 경우, 1번 노드를 거쳐가는 간선만을 업데이트하고 1 → 2, 3 → 1과 같이 직접 연결된 간선은 업데이트하지 않음 

## 동작 과정
1. 최단 거리 2차원 인접 행렬 구성 및 초기화
2. 거쳐가는 노드를 선택
3. 경로 간의 Relaxation을 통해 최단거리 업데이트
4. 위의 2, 3번 과정을 정점 수만큼 반복

### 예시

## 시간 복잡도
- 정점 수만큼 반복분이 3중으로 수행되기에 $O(V^3)$
  - 세제곱 시간 복잡도을 사용해도 되는 경우에만 사용 가능, V가 커질수록 매우 비효율적
  
> ⬆️:[Top](#플로이드-워샬Floyd-Warshall-알고리즘)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EC%B5%9C%EB%8B%A8%20%EA%B2%BD%EB%A1%9C(Shortest%20path)%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md#%EB%8B%A8%EC%9D%BC-%EC%8B%9C%EC%9E%91%EC%A0%90-%EC%B5%9C%EB%8B%A8-%EA%B2%BD%EB%A1%9C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
