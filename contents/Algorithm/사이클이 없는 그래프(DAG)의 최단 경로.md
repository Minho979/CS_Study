# 사이클이 없는 그래프(DAG)의 최단 경로
## 개념
- 그래프의 한 정점에서 다른 정점까지의 최단 경로를 구하는 알고리즘
- DAG에서의 최단경로는 선형시간에 간단하게 구할 수 있다.

## 동작 과정
1. 위상 정렬을 통해서 방문 순서대로 정점을 정렬
2. 각 정점마다 Relaxation을 통해 해당 정점과 연결되어 있는 정점들 중 최단거리를 찾는다.

### 예시 
- 위상 정렬이 끝난 예시 그래프
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DAGShortestEx1.png' width='500'>

1. 모든 정점의 가중치를 초기화하고 시작 노드의 가중치를 0으로 설정
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DAGShortestEx2.png' width='500'>

2. 시작 정점과 연결된 정점에 대해 Relaxation 수행 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DAGShortestEx3.png' width='500'>

- A와 연결된 정점 B의 가중치 비교
  - B: INF > 5 => 5로 갱신

3. B와 연결된 정점에 대해 Relaxation 수행
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DAGShortestEx4.png' width='500'>

- B와 연결된 C, D에 대해 가중치 비교
  - C: INF > 5 + 4 => 9로 갱신
  - D: INF > 5 + 7 => 12로 갱신

4. C와 열결된 정점에 대해 Relaxation 수행
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DAGShortestEx5.png' width='500'>

- C와 연결된 D, E에 대해 가중치 비교
  - D: 12 < 9 + 6 => 갱신 X 
  - E: INF > 9 + 4 => 13으로 갱신

5. D와 연결된 정점에 대해 Relaxation 수행
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DAGShortestEx6.png' width='500'>

- D와 연결된 E에 대해 가중치 비교
  - E: 13 < 12 + 3 => 갱신 X
 
6. E와 연결된 간선이 없기에 종료
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DAGShortestEx6.png' width='500'>


## 시간 복잡도
- 정점 수: V, 간선 수: E
- 위상 정렬을 수행하는 시간: $𝛩(V+E)$
- 모든 정점을 초기화하는 시간: $𝛩(V)$
- 각 정점에 대한 Relaxation을 수행하는 시간 $𝛩(|E|)$
- 최종적으로 위의 연산을 모두 합친  $𝛩(V+E)$

> ⬆️:[Top](#사이클이-없는-그래프DAG의-최단-경로)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EC%B5%9C%EB%8B%A8%20%EA%B2%BD%EB%A1%9C(Shortest%20path)%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md#%EB%8B%A8%EC%9D%BC-%EC%8B%9C%EC%9E%91%EC%A0%90-%EC%B5%9C%EB%8B%A8-%EA%B2%BD%EB%A1%9C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[알고리즘 정리] DAG에서 최단경로를 찾는 법](https://jeonyeohun.tistory.com/99)
