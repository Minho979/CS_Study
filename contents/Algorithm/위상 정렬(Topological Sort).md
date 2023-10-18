# 위상 정렬(Topological Sort)
## 개념
- 순서가 정해져 있는 작업들을 차례로 수행해야 할 때, 순서를 결정하는 알고리즘
  - 모든 정점을 일렬로 나열하되 정점 A에서 정점 B로 가는 간선이 있으면 A를 B보다 앞에 놓이도록 한다.
  - in-degree: 정점 A가 수행되기 전에 수행되어야할 정점 개수, out-degree: 정점 A가 먼저 수행되어야 할 수 있는 정점 개수
  - 즉, 진입 차수가 0인 정점부터 수행한다.
- 하나의 DAG에 하나 이상의 위상 순서가 존재한다.
  - 위상 정렬의 결과는 여러 가지일 수 있다.
- 구현 방법으로는 BFS(진입 차수), DFS(진출 차수)를 이용하는 2가지 방법이 존재한다.

## 조건
- Cycle이 없는 유향 그래프(DAG: Directed Acyclic Graph)에만 적용이 가능하다.
  - 사이클이 있을 경우 시작 정점을 정할 수 없기 때문에 적용이 불가

## BFS를 이용한 위상 정렬
### 개념
- 진입 차수가 0인 정점을 큐에 차례로 삽입하여 FIFO 구조를 이용하여 위상 정렬을 진행한다.
- 최종 결과에서 사이클의 유무를 판단
  - 큐가 비어있는 상황에서 결과의 길이가 정점 수보다 적은 경우 사이클이 존재한다.

### 수행 과정
1. 진입 차수가 0인 시작 정점 한 개를 큐에 삽입한다.
2. 큐가 비어있지 않다면 정점 한 개를 꺼내 결과 리스트에 삽입한다. 만약 큐가 비어있다면 종료한다.
3. 꺼낸 정점과 인접한 모든 정점의 진입 차수를 -1만큼 감소시키고 꺼낸 정점을 결과 리스트에 삽입한다.

   3-1. 감소한 진입 차수가 0이라면 이 정점은 새로운 시작 정점이 될 수 있기에 큐에 삽입한다.

### 예시
- 사용된 그래프 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-Graph.jpg' width='500'>
1. 진입 차수가 0인 A를 큐에 삽입한다.
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-BFS1.jpg' width='500'>
2. A를 꺼내고 인접 정점의 진입 차수를 1씩 감소 시킨 다음 A를 결과 리스트에 삽입한다. 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-BFS2.jpg' width='500'>
3. 진입 차수가 0인 정점 B, D를 큐에 삽입한다.
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-BFS3.jpg' width='500'>
4. B를 꺼내고 인접 정점의 진입 차수를 1씩 감소 시킨 다음 B를 결과 리스트에 삽입한다.
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-BFS4.jpg' width='500'>
5. D를 꺼내고 인접 정점의 진입 차수를 1씩 감소 시킨 다음 D를 결과 리스트에 삽입한다.
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-BFS5.jpg' width='500'>
6. 진입 차수가 0인 C를 큐에 삽입한다.
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-BFS6.jpg' width='500'>
7. C를 꺼내고 인접 정점의 진입 차수를 1씩 감소 시킨 다음 C를 결과 리스트에 삽입한다.
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-BFS7.jpg' width='500'>
8. 진입 차수가 0인 F, G를 큐에 삽입한다.
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-BFS8.jpg' width='500'>
9. F를 꺼내고 인접 정점의 진입 차수를 1씩 감소 시킨 다음 F를 결과 리스트에 삽입한다.
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-BFS9.jpg' width='500'>
10. 진입 차수가 0인 E를 큐에 삽입한다.
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-BFS10.jpg' width='500'>
11. G를 꺼내고 인접 정점이 없기에 결과 리스트에 G를 삽입한다. E에 대해서도 같은 작업을 수행한다.
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-BFS11.jpg' width='500'>


### 시간 복잡도 
- 인접 리스트 그래프의 모든 노드를 확인하면서 $O(V)$, 해당 노드에서 출발하는 간선을 제거한다. $O(E)$
- 모든 노드와 간선을 확인하기에 $O(V + E)$ 
- 인접 행렬을 이용하는 경우 $O(V^2)$

### 구현
``` java
class MyGraphBFS {
	int vertexCnt;
	int[] in_Degree;
	ArrayList<Integer>[] edge_List;
	
	public MyGraphBFS(int N) {
		this.vertexCnt = N;
		edge_List = new ArrayList[N+1];
		for (int i = 0; i <= N; ++i) {
			edge_List[i] = new ArrayList<>();
		}
		in_Degree = new int[vertexCnt+1];
	}

	public void insert_Edge(int from, int to) {
		edge_List[from].add(to);

		//to의 진입 차수 증가
		in_Degree[to]++;
	}

	public void topological_Sort_BFS() {
		Queue<Integer> q = new LinkedList<>();
		
		//진입 차수가 0인 정점들을 큐에 넣어줌
		for (int i = 1; i <= vertexCnt; ++i) {
			if (in_Degree[i] == 0) {
				q.offer(i);
			}
		}
		
		//결과의 크기는 정점의 수여야 하기 떄문에 정점의 수만큼 반복 
		for (int i = 1; i <= vertexCnt; ++i) {
			//다 돌기전에 큐가 비었다는 것은 사이클이 존재한다는 것을 의미
			if (q.isEmpty()) {
				System.out.println("그래프에 사이클이 존재");
				return;
			}
			
			int v = q.poll();
			System.out.print(v + " ");
			
			for (int j = 0; j < edge_List[v].size(); ++j) {
				int nv = edge_List[v].get(j);
				
				//인접한 정점의 진입 차수를 -1만큼 감소하고 0이면 큐에 넣어준다.
				if (--in_Degree[nv] == 0) {
					q.offer(nv);
				}
			}
		}
	}
}

public class TopologicalSort {

	public static void main(String[] args) {
		MyGraphBFS mgb = new MyGraphBFS(7);
		mgb.insert_Edge(1, 2);
		mgb.insert_Edge(1, 3);
		mgb.insert_Edge(1, 4);
		mgb.insert_Edge(2, 5);
		mgb.insert_Edge(2, 6);
		mgb.insert_Edge(3, 7);
		mgb.insert_Edge(3, 6);
		mgb.insert_Edge(4, 3);
		mgb.insert_Edge(6, 5);
		mgb.topological_Sort_BFS();
		
	}
}
```
- 출력 결과
`1 2 4 3 7 6 5`
  - 각 숫자는 A~E까지의 순서를 의미 1: A, 2: B, 3: C, 4: D, 5: E, 6: F, 7: G

## DFS를 이용한 위상 정렬
### 개념
- DFS를 이용하여 말단 노드까지 내려가 진출 차수가 0인 정점을 스택에 삽입하여 LIFO 구조를 이용하여 위상 정렬을 진행한다.
  - 진출 차수가 0인 정점은 가장 마지막에 수행되는 정점
- DFS의 수행으로 인해 가장 더 늦게 수행되어야 하는 정점이 스택에 먼저 삽입되기 때문에 방문하지 않은 정점 중 랜덤하게 선택해도 문제가 발생하지 않는다.
- DAG 확인을 위해 사이클의 유무를 판단할 수 있어야 한다.
  - 이를 위해 DFS 수행 중 방문 정점에 방문 처리를 진행한다.
  - DFS 수행 중 방문 처리가 된 노드가 있다면 사이클이 존재하는 것을 의미한다.
  - 이를 위해 별도의 배열을 생성하여 DFS가 완전히 끝날 때를 표시하고 사이클의 유무를 판단한다.

### 수행 과정
1. 임의의 방문하지 않은 정점을 선택하여 DFS를 수행하면서 방문하는 정점들을 스택에 삽입하고 방문처리를 해준다.
   - 스택에 삽입하는 정점은 더이상 DFS를 수행할 수 없는 정점을 삽입
2. 모든 정점의 방문을 완료할 때까지 1번을 반복한다.
3. 모든 정점을 방문한 했다면 스택에 삽입한 정점들을 출력하고 위상 정렬을 종료한다.

### 예시
- 사용된 그래프 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-Graph.jpg' width='500'>
1. 임의의 정점 B를 선택하고 B에 대한 DFS를 수행한다. 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-DFS1.jpg' width='500'>

- E에서 더 이상 방문할 곳이 없기에 E를 스택에 삽입한다.
  
2. B에 대한 DFS를 계속 진행한다. 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-DFS2.jpg' width='500'>

- F에서 더 이상 방문할 곳이 없기에 F를 스택에 삽입하고, B 또한 같은 이유로 스택에 삽입한다.

3. 방문하지 않은 정점 A에 대해 DFS를 수행한다. 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-DFS3.jpg' width='500'>

- A-C-G 순서로 방문하고 G에서 방문할 정점이 없기에 G를 스택에 삽입한다.
- 정점 C도 마찬가지로 스택에 삽입한다.

4. A에 대해 DFS를 계속 진행한다.
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Topological-DFS4.jpg' width='500'>

- D를 방문 한 후 스택에 삽입하고 A 또한 스택에 삽입한다.

### 시간 복잡도 
- 인접 리스트 그래프의 모든 노드를 확인하면서 $O(V)$, 해당 노드에 진입하는 간선을 제거한다. $O(E)$
- 모든 노드와 간선을 확인하기에 $O(V + E)$ 
- 인접 행렬을 이용하는 경우 $O(V^2)$

### 구현 
``` java
class MyGraphDFS {
	int vertexCnt;
	ArrayList<Integer>[] edge_List;
	boolean[] visit;
	boolean[] finish;
	Stack<Integer> answer;
	boolean cycle;
	
	public MyGraphDFS(int N) {
		this.vertexCnt = N;
		edge_List = new ArrayList[N+1];
		for (int i = 0; i <= N; ++i) {
			edge_List[i] = new ArrayList<>();
		}
		visit = new boolean[vertexCnt+1]; //방문 표시
		finish = new boolean[vertexCnt+1]; //사이클 판단
		answer = new Stack<>(); //결과를 담을 스택
	}

	public void insert_Edge(int from, int to) {
		edge_List[from].add(to);
	}

	public void topological_Sort_DFS() {
		//방문하지 않은 정점을 DFS 수행
		for (int i = 1; i <= vertexCnt; ++i) {
			if (cycle) {
				System.out.println("그래프에 사이클 존재");
				return;
			}
			if (!visit[i]) {
				dfs(i);
			}
		}
		
		//스택에 담긴 정점들을 출력
		while (!answer.isEmpty()) {
			System.out.print(answer.pop() + " ");
		}
	}
	
	public void dfs(int v) {
		visit[v] = true;
	
		for (int i = 0; i < edge_List[v].size(); ++i) {
			int nv = edge_List[v].get(i);
			
			//방문하지 않았으면 dfs 수행
			if (!visit[nv]) {
				dfs(nv);
			} 
			//방문한 정점인데 finish 체크가 되지 않았으면 사이클이 존재한다는 의미
			else if (!finish[nv]) {
				cycle = true;
				return;
			}
		}
		
		//더 이상 갈 곳이 없는 정점을 finish 체크 & 스택에 넣어줌 (말단부터 상위로)
		finish[v] = true;
		answer.push(v);
	}
}

public class TopologicalSort {

	public static void main(String[] args) {
		MyGraphDFS mgd = new MyGraphDFS(7);
		mgd.insert_Edge(1, 2);
		mgd.insert_Edge(1, 3);
		mgd.insert_Edge(1, 4);
		mgd.insert_Edge(2, 5);
		mgd.insert_Edge(2, 6);
		mgd.insert_Edge(3, 7);
		mgd.insert_Edge(3, 6);
		mgd.insert_Edge(4, 3);
		mgd.insert_Edge(6, 5);
		mgd.topological_Sort_DFS();
```
- 출력 결과
`1 4 3 7 2 6 5`
  - 각 숫자는 A~E까지의 순서를 의미 1: A, 2: B, 3: C, 4: D, 5: E, 6: F, 7: G

> ⬆️:[Top](#위상-정렬Topological-Sort)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [위상 정렬(Topological Sort)](https://sorjfkrh5078.tistory.com/36)
