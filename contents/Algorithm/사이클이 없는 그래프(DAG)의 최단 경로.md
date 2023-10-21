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

## 구현
``` java
public class DAG_Shortest_Path {
	
	static final int INF = Integer.MAX_VALUE;	// 초기화 상수 
	
	static class Node {
		int from;
		int to;
		int cost;
		
		Node(int from, int to, int cost) {
			this.from = from;
			this.to = to;
			this.cost = cost;
		}
	}
	
	// 거리, 그래프 간선, 진입 차수, 시작 정점, 정점 개수 
	public static int[] DAG_ShortestPath  (int[] dist, List<List<Node>> edge, int[] in_degree, int start, int n) {
		int to;
		int cost;
		
		StringBuilder sb = new StringBuilder();
		
		// dist 초기화 
		Arrays.fill(dist, INF);
		
		// 시작 노드 초기화 
		dist[start] = 0;
		
		// 위상 정렬 수행 
		int[] topological = new int[n+1];	// 0번 인덱스는 사용하지 않음 
		int idx = 0;
		
		PriorityQueue<Integer> pq = new PriorityQueue<>();
		
		// 진입 차수 0인 정점 큐에 삽입 
		for (int i = 0; i <= n; ++i) {
			if (in_degree[i] == 0) {
				pq.add(i);
			}
		}
		
		// 정점 수 만큼 반복 
		for (int i = 0; i <= n; ++i) {
			int v = pq.remove();
			
			// 방문 순서 문자열 만들기 
			sb.append(v + " ");
			
			// 위상 정렬 배열에 방문 순서대로 정점 삽입 
			topological[idx++] = v;
			for (Node node : edge.get(v)) {
				to = node.to;
				if (--in_degree[to] == 0) {
					pq.add(to);
				}
			}
		}
		
		// 위상 정렬 된 배열 순서대로 반복  
		for (int v: topological) {
			for (Node node : edge.get(v)) {
				to = node.to;
				cost = node.cost;
				if (dist[v] == INF) continue;

				// Relaxation 수행 
				if (dist[to] > dist[v] + cost) {
					dist[to] = dist[v] + cost;
				}
			}
		}
		
		// 방문 순서 출력 및 거리 리턴 
		System.out.println("방문 순서: " + sb.toString());
		return dist;
		
		
	}
	
	public static void main(String[] args) {
		int n = 5;		// 정점 수 
		int start = 1;	// 시작 정점 
		
		
		int[] dist = new int[n + 1]; // 최종 거리 배열, 0번 인덱스는 사용하지 않음 
		
		List<List<Node>> edge = new LinkedList<>();
		
		for (int i = 0; i <= n; ++i) {
			edge.add(new LinkedList<Node>());
		}
		
		// 간선 정보 입력 
		edge.get(1).add(new Node(1, 2, 5));
		edge.get(2).add(new Node(2, 3, 4));
		edge.get(2).add(new Node(2, 4, 7));
		edge.get(3).add(new Node(3, 4, 6));
		edge.get(3).add(new Node(3, 5, 4));
		edge.get(4).add(new Node(4, 5, 3));
		
		// 진입 차수 입력 
		int[] in_degree = new int [n + 1];
		in_degree[2] ++;
		in_degree[3] ++;
		in_degree[4] ++;
		in_degree[4] ++;
		in_degree[5] ++;
		in_degree[5] ++;
		
		// DAG_ShortestPath 호출 
		dist = DAG_ShortestPath (dist, edge,in_degree, start, n);
		
		StringBuilder sb = new StringBuilder();
		for (int i : dist) {
			sb.append((i == INF ? "INF" : i) + " ");
		}
		
		System.out.println("최소 거리: " + sb.toString());

	}

}
```


> ⬆️:[Top](#사이클이-없는-그래프DAG의-최단-경로)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EC%B5%9C%EB%8B%A8%20%EA%B2%BD%EB%A1%9C(Shortest%20path)%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md#%EB%8B%A8%EC%9D%BC-%EC%8B%9C%EC%9E%91%EC%A0%90-%EC%B5%9C%EB%8B%A8-%EA%B2%BD%EB%A1%9C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[알고리즘 정리] DAG에서 최단경로를 찾는 법](https://jeonyeohun.tistory.com/99)
> - [[알고리즘] 그래프 최단 경로 ( Shortest Path ) - 다익스트라, 벨만-포드, 플로이드-워샬, 사이클이 없는 유향 그래프( DAG )](https://hyunjiishailey.tistory.com/233)
