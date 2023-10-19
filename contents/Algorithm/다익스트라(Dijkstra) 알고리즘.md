# 다익스트라(Dijkstra) 알고리즘
## 개념 
- 그래프의 한 정점에서 다른 정점까지의 최단 경로를 구하는 알고리즘
- 도착 정점 뿐만 아니라 모든 다른 정점까지 최단 경로로 방문하여 각 정점까지의 최단 경로를 모두 찾는다.
- 최소 신장 트리를 위한 Prim 알고리즘과 원리가 비슷하다.
  - [Prim 알고리즘](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/Prim%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md)
  - Prim 알고리즘에서는 d[v]가 정점 v를 신장 트리에 연결하는 최소 비용
  - 다익스트라 알고리즘에서는 d[v]가 시작 정점에서 도착 정점에 이르는 최단 거리

## 조건
- 그래프의 모든 간선 가중치는 음(-)이 아니어야 한다.

## 동작 과정
1. 출발 노드와 도착 노드를 설정
2. '최단 거리 테이블' 초기화
3. 현재 위치한 노드의 인접 노드 중 방문하지 않는 노드 중 거리가 가장 짧은 노드를 선택 후 방문 처리
4. 해당 노드를 거쳐 다른 노드로 넘어가는 가중치를 계산해 '최단 거리 테이블' 업데이트
5. 최종 결과가 나올때 까지 3, 4번 과정을 반복한다.

### 예시
1. 출발 노드, 도착 노드 설정 및 가중치 초기화
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Dijkstra-Ex1.png' width='500'>
2. 출발 노드를 선택하고 가중치 0으로 설정
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Dijkstra-Ex2.png' width='500'>
3. 1번 노드와 연결된 인접 노드의 기존의 가중치와 부여된 가중치를 비교하고 최솟값으로 업데이트 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Dijkstra-Ex3.png' width='500'>

- 인접 노드까지의 거리를 모두 업데이트한 1번 노드는 방문 처리

4. 방문하지 않은 노드 중 거리가 가장 짧은 4번 노드 방문
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Dijkstra-Ex4.png' width='500'>

- 4번 노드와 인접한 노드의 가중치를 비교하여 최솟값으로 업데이트
- 2번 노드의 경우 기존의 거리 2와 4번을 거쳐가는 1+2 = 3을 비교하고 신규 값이 더 크므로 업데이트를 진행하지 않음
- 인접 노드까지의 거리를 모두 업데이트한 4번 노드는 방문 처리

5. 방문하지 않은 노드 중 거리가 가장 짧은 2번 노드 방문
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Dijkstra-Ex5.png' width='500'>

- 2번 노드와 인접한 노드의 가중치를 비교하여 최솟값으로 업데이트
- 4번 노드의 경우 기존 거리 1보다 2를 거쳐가는 2+2 = 4가 더 크기에 업데이트를 진행하지 않음
- 인접 노드까지의 거리를 모두 업데이트한 2번 노드는 방문 처리

6. 방문하지 않은 노드 중 거리가 가장 짧은 5번 노드 방문
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Dijkstra-Ex6.png' width='500'>

- 5번 노드와 인접한 노드의 가중치를 비교하여 최솟값으로 업데이트
- 인접 노드까지의 거리를 모두 업데이트한 5번 노드는 방문 처리

7. 방문하지 않은 노드 중 거리가 가장 짧은 6번 노드 방문
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Dijkstra-Ex7.png' width='500'>

- 최종 도착 노드이기 때문에 알고리즘을 종료
- 1 - 4 - 5 - 6의 경로를 지나며 최소 거리는 4가 된다.

## 시간 복잡도
- 노드의 개수: V
- 인접 행렬을 이용한 경우: $O(V^2)$
  - 2차원 배열을 순차 탐색을 통해 가장 작은 노드를 찾음
- 우선순위 큐를 이용한 경우: $O(E log V)$
  - 연결 노드를 탐색하는 시간 $O(E)$, 큐에 삽입하는 시간 $O(log V)$
 
## 구현
``` java
class Node implements Comparable<Node>{
	int index;
	int cost;
	
	public Node(int index, int cost) {
		this.index = index;
		this.cost = cost;
	}

	@Override
	public int compareTo(Node o) {
		return Integer.compare(this.cost, o.cost);
	}
}

public class Dijkstra {
	// 그래프를 표현 List
	static ArrayList<Node>[] graph;
	
    //노드의 크기, 출발지
	public static void Dijkstra(int v, int start) {
		int[] dist = new int[v + 1]; // 최단 거리 저장 변수, 0번 인덱스는 사용하지 않음 
		int INF = Integer.MAX_VALUE;
		
		PriorityQueue<Node> pq = new PriorityQueue<>();
		
		// dist 초기화 
		Arrays.fill(dist, INF);
		
		// 시작 노드 값 초기화 
		dist[start] = 0;
		pq.offer(new Node(start, 0));
		
		while(!pq.isEmpty()) {
			// 노드 꺼내기
			Node node = pq.poll();
			int nodeIndex = node.index; // 꺼낸 노드의 인덱스 
			int cost = node.cost;		// 꺼낸 노드의 가중치 
			
			/*
			 우선순위 큐는 cost를 기준으로 오름차순으로 정렬되는 상태 
			 현재 꺼낸 노드의 가중치가 최단 거리 테이블의 값보다 크다면 
			 해당 노드는 이전에 방문된 노드이므로,
			 해당 노드와 인접한 노드를 탐색하지 않고 큐에서 다음 노드를 꺼낸다.
			 cost = 6, dist[nodeIndex] = 3 인 경우, 
			 누적 가중치 3의 경로로 이미 방문한 상태 
			 */
			if(cost > dist[nodeIndex]) continue;
			
			// 현재 노드와 연결된 정점 비교
			for(Node next : graph[nodeIndex]) {
				if(dist[next.index] > dist[nodeIndex]+ next.cost) {
					// 최단 경로 테이블 갱신 
					dist[next.index] = dist[nodeIndex] + next.cost;
					// 갱신된 노드 삽입 
					pq.offer(new Node(next.index, dist[next.index]));
				}
			}
		}
        
        // 최소거리 출력
		for(int i : dist) {
			if(i == INF) System.out.print("INF ");
			else System.out.print(i+" ");
		}
	}

	public static void main(String[] args) throws IOException {
    
		// 그래프 입력 받기
		BufferedReader bf = new BufferedReader(new InputStreamReader(System.in));
		// 정점의 개수, 간선의 개수
		int v = Integer.parseInt(bf.readLine());
		int e = Integer.parseInt(bf.readLine());
		
		graph = new ArrayList[v+1]; // 0번 인덱스는 이용하지 않음 
		for (int i = 0; i <= v; i++)  graph[i] = new ArrayList<>();
		
		StringTokenizer st;
		for(int i = 0 ; i < e; i++) {
			st = new StringTokenizer(bf.readLine());
			int from = Integer.parseInt(st.nextToken());
			int to = Integer.parseInt(st.nextToken());
			int cost = Integer.parseInt(st.nextToken());
			
			graph[from].add(new Node(to, cost));
		}

		int start = 1;

		// 다익스트라 알고리즘 수행
		Dijkstra(v, start);
		
	}
}
```
``` java 
입력 값
6      // (정점 수)
7      // (간선 수)
1 2 2  // (from to cost)
1 4 1  // (from to cost)
4 2 2  // (from to cost)
4 5 1  // (from to cost)
2 3 3  // (from to cost)
3 6 5  // (from to cost)
5 6 2  // (from to cost)

출력 값
/*
 0  1 2 3 4 5 6 */
INF 0 2 5 1 2 4 // 0번 인덱스는 이용하지 않음 (정점의 이름과 인덱스를 맞추기 위해)
```

> ⬆️:[Top](#다익스트라Dijkstra-알고리즘)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EC%B5%9C%EB%8B%A8%20%EA%B2%BD%EB%A1%9C(Shortest%20path)%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md#%EB%8B%A8%EC%9D%BC-%EC%8B%9C%EC%9E%91%EC%A0%90-%EC%B5%9C%EB%8B%A8-%EA%B2%BD%EB%A1%9C-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[알고리즘] 다익스트라(Dijkstra) 알고리즘](https://velog.io/@717lumos/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EB%8B%A4%EC%9D%B5%EC%8A%A4%ED%8A%B8%EB%9D%BCDijkstra-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98)
> - [[알고리즘/Java]다익스트라(Dijkstra) 알고리즘](https://velog.io/@suk13574/알고리즘Java다익스트라Dijkstra-알고리즘)
