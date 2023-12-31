# 벨만-포드(Bellman-Ford) 알고리즘
## 개념
- 그래프의 한 정점에서 다른 정점까지의 최단 경로를 구하는 알고리즘
- `정점 수 - 1`번의 매 단계마다 모든 간선을 전부 확인하면서 모든 노드간의 최단 거리를 구한다.
- 간선 가중치의 범위가 임의의 실수로 음의 가중치인 경우에도 사용이 가능하다.

## 동작 과정
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Bellman%E2%80%93Ford_algorithm_example.gif' width='500'>

1. 출발 노드를 설정
2. '최단 거리 테이블' 초기화
3. 다음 과정을 `정점 수 - 1`번 반복
   
    3-1. 모든 간선 E개를 하나씩 확인

    3-2. 각 간선을 거쳐 다른 노드로 가는 비용을 계산하여 최단 거리 테이블을 갱신

4. 음수 간선 순환이 발생하는지 3번 과정을 한번 더 수행하여 확인
    - (정점 수)번째의 3번 과정 수행
    - 이때 최단 거리 테이블이 갱신된다면 음수 간선 순환이 존재

### 예시

- 예시에 사용되는 그래프 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Bellman-Ford-Ex1.png' width='600'>

- 정점 수: `n = 5`, 간선 수: `m = 9`
- v: 간선 진출 정점(from)
- w: 간선 진입 정점(to)
- cost: 비용(거리)
- dist: 최단 거리 테이블
- 출발 노드: 4

1. iteration = 1 (간선 최대 1개를 사용하는 최단 경로)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Bellman-Ford-Ex2.png' width='600'>

- 정점 4의 진출 간선을 살펴본 후 dist의 최솟값을 업데이트 해준다.
- `dist[1] = 8`, `dist[5] = 3`
  - `dist[1] = INF` > `dist[4] + cost[4, 1] = 8` => 8로 업데이트
  - `dist[5] = INF` > `dist[4] + cost[4, 5] = 3` => 3으로 업데이트

2. iteration = 2 (간선 최대 2개를 사용하는 최단 경로)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Bellman-Ford-Ex3.png' width='600'>

- 정점 1, 4, 5의 간선을 살펴본 후 dist의 최솟값을 업데이트 해준다.
- `dist[2] = 18`, `dist[3] = 13`
  - `dist[2] = INF` > `dist[1] + cost[1, 2] = 18` => 8로 업데이트
  - `dist[3] = INF` > `dist[1] + cost[1, 3] = 13` => 3으로 업데이트
  - `dist[4] = 0` < `dist[5] + cost[5, 4] = 12` => 유지
  - `dist[2] = 18` < `dist[5] + cost[5, 2] = 34` => 유지

3. iteration = 3 (간선 최대 3개를 사용하는 최단 경로)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Bellman-Ford-Ex4.png' width='600'>

- 모든 정점의 간선을 살펴보며 위의 과정을 `정점 수(n) - 1`번 수행한다.
- 음수 간선 순환이 확인하기 위해 모든 간선에 대해 'n`번째의 연산을 수행한다.

4. 최종 결과
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Bellman-Ford-Ex5.png' width='600'>

- 음수 사이클 예시 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Bellman-Ford-cycle-Ex.png' width='600'>

   - 위의 그림처럼 음수 가중치가 포함된 사이클이 있는 경우 음수 사이클이 존재하는 것이다.
   - 해당 사이클의 존재 여부를 확인하기 위해 `정점 수`번째의 반복하는 과정을 한번 더 진행한다.
   - 해당 과정에서 값이 변화가 일어나면 음수 사이클이 존재하는 것이다

## 시간 복잡도
- 정점 수: V. 간선 수: E 
- `정점 수 - 1`개 만큼 사이클을 돌고 각 사이클 마다 간선을 확인하므로 $O(|V-1||E|)$ 
- $O(|V||E|)$

## 구현 
``` java
class Edge {
	int v;    // 나가는 정점
	int w;    // 들어오는 정점
	int cost;

	public Edge(int v, int w, int cost) {
		this.v = v;
		this.w = w;
		this.cost = cost;
	}
}

public class Bellman_Ford {
	static ArrayList<Edge> graph;
	static final int INF = Integer.MAX_VALUE;
	
	// 정점의 개수, 간선의 개수, 출발지
	public static boolean BellmanFord(int n, int m, int start) {
		int[] dist = new int[n + 1]; 	  // 0번 인덱스 사용 안함 
		Arrays.fill(dist, INF);		  // 테이블 초기화 
		dist[start] = 0;		  // 출발 노드 가중치 0 

		// 정점의 개수만큼 반복
		for (int i = 0; i < n; i++) {
			// 간선의 개수만큼 반복
			for (int j = 0; j < m; j++) {
				Edge edge = graph.get(j); // 현재 간선
				
				// 현재 간선의 들어오는 정점에 대해 비교
				// edge.v = 정점에서 나가는 간선, edge.w 정점으로 들어오는 간선 
				if (dist[edge.v] != INF && dist[edge.w] > dist[edge.v] + edge.cost) {
					dist[edge.w] = dist[edge.v] + edge.cost;
				}
			}
		}
		
		// n번 반복 후 음수 가중치 확인
		for (int i = 0; i < m; i++) {
			Edge edge = graph.get(i); // 현재 간선
			
			// 현재 간선의 들어오는 정점에 대해 비교 -> 더 작은 값 생기면 음수 사이클 존재
			if (dist[edge.v] != INF && dist[edge.w] > dist[edge.v] + edge.cost) {
				System.out.println("음수 사이클 존재");
				return false;
			}
		}
		
		// 출력
		for (int i = 1; i < dist.length; i++) {
			if (dist[i] == INF)
				System.out.print("INF ");
			else
				System.out.print(dist[i] + " ");
		}
		
		return true;
	}

	public static void main(String[] args) throws IOException {
    
		// 그래프 입력받기
		BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
		// 정점의 개수, 간선의 개수 
		int n = Integer.parseInt(bf.readLine());
		int m = Integer.parseInt(bf.readLine());

		graph = new ArrayList<>();

		StringTokenizer st;
		for (int i = 0; i < m; i++) {
			st = new StringTokenizer(bf.readLine());
			int v = Integer.parseInt(st.nextToken());
			int w = Integer.parseInt(st.nextToken());
			int cost = Integer.parseInt(st.nextToken());

			graph.add(new Edge(v, w, cost));
		}
		
       	 	// 벨만-포드 알고리즘 수행
		BellmanFord(n, m, 4);
	}
}
```
- 음수 사이클이 없는 그래프의 경우
``` java
입력 값
5	// 정점 수 
9	// 간선 수
1 2 10	// (from, to, cost)
1 3 5	// (from, to, cost)
2 3 2	// (from, to, cost)
3 1 1	// (from, to, cost)
3 2 13	// (from, to, cost)
4 1 8	// (from, to, cost)
4 5 3	// (from, to, cost)
5 4 9	// (from, to, cost)
5 2 31	// (from, to, cost)

출력 값
/*
1  2  3 4 5 */
8 18 13 0 3 
```
- 음수 사이클이 있는 그래프의 경우
``` java
입력 값 
5	// 정점 수 
9	// 간선 수
1 2 -10	// (from, to, cost)
1 3 5	// (from, to, cost)
2 3 2	// (from, to, cost)
3 1 1	// (from, to, cost)
3 2 13	// (from, to, cost)
4 1 8	// (from, to, cost)
4 5 3	// (from, to, cost)
5 4 9	// (from, to, cost)
5 2 31	// (from, to, cost)

출력 값
음수 사이클 존재
```

> ⬆️:[Top](#벨만-포드Bellman-Ford-알고리즘)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EC%B5%9C%EB%8B%A8%20%EA%B2%BD%EB%A1%9C(Shortest%20path)%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md#%EB%8B%A8%EC%9D%BC-%EC%8B%9C%EC%9E%91%EC%A0%90-%EC%B5%9C%EB%8B%A8-%EA%B2%BD%EB%A1%9C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [벨먼-포드 알고리즘](https://ko.wikipedia.org/wiki/%EB%B2%A8%EB%A8%BC-%ED%8F%AC%EB%93%9C_%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
> - [[알고리즘/Java] 벨만-포드(Bellman-Ford) 알고리즘](https://velog.io/@suk13574/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98Java-%EB%B2%A8%EB%A7%8C-%ED%8F%AC%EB%93%9CBellman-Ford-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
