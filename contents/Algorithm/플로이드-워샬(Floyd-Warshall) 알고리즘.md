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
- 예시에 이용된 그래프
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Floyd-Warshall-Graph.png' width='500'>

1. 그래프를 2차원 인접 행렬로 구성 및 초기화
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Floyd-Warshall-Ex1.png' width='500'>

- 직접 연결된 간선에 대한 값만을 삽입 후 나머지 값은 INF로 초기화

2. 1번 노드를 경유지 노드로 설정 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Floyd-Warshall-Ex2.png' width='650'>

- 1번 노드를 경유해 지나가는 경우 갈 수 있는 경로는 (3 → 2), (4 → 2)
- 3번에서 2번으로 가는 경우 `min(INF, 10 + 3)` => 13으로 업데이트
- 4번에서 2번으로 가는 경우 `min(INF, 2 + 10 + 3)` => 15로 업데이트

3. 2번 노드를 경유지 노드로 설정
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Floyd-Warshall-Ex3.png' width='650'>

- 2번 노드를 경유해 지나가는 경우 갈 수 있는 경로는 (1 → 3), (1 → 4), (3 → 4)
- 1번에서 3번으로 가는 경우 `min(10, 3 + 4)` => 7로 업데이트
- 1번에서 4번으로 가는 경우 `min(INF, 3 + 1)` => 4로 업데이트
- 3번에서 4번으로 가는 경우 `min(INF, 10 + 3 + 1)` => 14로 업데이트

4. 3번 노드를 경유지 노드로 설정
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Floyd-Warshall-Ex4.png' width='650'>

- 3번 노드를 경유해 지나가는 경우 갈 수 있는 경로는 (2 → 1), (4 → 1)
- 2번에서 1번으로 가는 경우 `min(INF, 4 + 10)` => 14로 업데이트
- 4번에서 1번으로 가는 경우 `min(INF, 2 + 10)` => 12로 업데이트

5. 4번 노드를 경유지 노드로 설정
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Floyd-Warshall-Ex5.png' width='650'>

- 4번 노드를 경유해 지나가는 경우 갈 수 있는 경로는 (1 → 3), (2 → 1), (2 → 3)
- 1번에서 3번으로 가는 경우 `min(7, 3 + 1 + 2)` => 6으로 업데이트
- 2번에서 1번으로 가는 경우 `min(14, 1 + 2 + 10)` => 13으로 업데이트
- 2번에서 3번으로 가는 경우 `min(4, 1 + 2)` => 3으로 업데이트

## 시간 복잡도
- 정점 수만큼 반복분이 3중으로 수행되기에 $O(V^3)$
  - 세제곱 시간 복잡도을 사용해도 되는 경우에만 사용 가능, V가 커질수록 매우 비효율적
 
## 구현 
``` java
public class Floyd_Warshall {
	
	// Integer.MAX_VALUE 이용 시 출력 오류가 발생하여 임의로 값 설정 
	static final int INF = 1000000000;
	
	// 그래프, 정점 수 
	public static void Floyd(int[][] graph, int v) {
		// 0번 인덱스는 사용하지 않아 1부터 값 비교 
		// 경유지 k
		for (int k = 1; k <= v; ++k) {
			// 출발지 i(행)
			for (int i = 1; i <= v; ++i) {
				// 도착지 j(열)
				for (int j = 1; j <= v; ++j) {
					// Relaxation 
					graph[i][j] = Math.min(graph[i][j], graph[i][k] + graph[k][j]);
				}
			}
		}
		
		// 출력, 0번 인덱스를 사용하지 않아 1부터 출력 
		for (int i = 1; i <= v; ++i) {
			for (int j = 1; j <= v; ++j) {
				if(graph[i][j] == INF) System.out.print("INF ");
				else System.out.print(graph[i][j] + " ");
			}
			System.out.println();
		}
	}

	public static void main(String[] args) throws IOException{
		int v = 4;	// 정점 수 
		
		int[][] graph = new int[v + 1][v + 1];	// 2차원 인접 행렬, 0번 인덱스 이용 x
		
		// 그래프 최단 거리 인접 행렬 초기화 
		for (int i = 1; i < graph.length; ++i) {
			for (int j = 1; j < graph.length; ++j) {
				if (i == j) continue;
				graph[i][j] = INF;
			}
		}
		
		// 데이터 삽입 
		graph[1][2] = 3;
		graph[1][3] = 10;
		graph[2][3] = 4;
		graph[2][4] = 1;
		graph[3][1] = 10;
		graph[4][3] = 2;
		
		// 플로이드-워샬 알고리즘 수행 
		Floyd(graph, v);
	}

}
```
``` java
출력 값
// 가독성을 위해 위치 조정
 0   3  6   4
13   0  3   1
10  13  0  14
12  15  2   0
```

  
> ⬆️:[Top](#플로이드-워샬Floyd-Warshall-알고리즘)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EC%B5%9C%EB%8B%A8%20%EA%B2%BD%EB%A1%9C(Shortest%20path)%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md#%EB%8B%A8%EC%9D%BC-%EC%8B%9C%EC%9E%91%EC%A0%90-%EC%B5%9C%EB%8B%A8-%EA%B2%BD%EB%A1%9C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
