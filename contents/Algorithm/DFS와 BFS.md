# 깊이우선탐색(DFS)와 너비우선탐색(BFS)
- 그래프를 탐색하는 알고리즘
  - 그래프 탐색: 하나의 정점에서 시작하여 차례대로 모든 정점들을 한 번씩 방문
  - [그래프(Graph)란?](https://github.com/Minho979/CS_Study/blob/main/contents/Data%20Structure/Graph.md)

## 깊이 우선 탐색(DFS, Depth-First Search)
### 개념
- 루트 노드(혹은 다른 임의의 노드)에서 시작하여 다음 분기(branch)로 넘어가기 전에 해당 분기를 완벽하게 탐색하는 방법
  - 미로를 탐색할 때 막다른 길이 나올때까지 한 방향으로 진행하다가 더 이상 진행이 불가능할 때 가장 가까운 갈림길로 돌아와 다른 방향으로 동일한 방식으로 진행하는 방법과 유사
  - 넓게(wide) 탐색하기 이전에 깊게(deep) 탐색
  - 모든 노드를 방문하고자 하는 경우 사용

### DFS의 특징
- 자기 자신을 호출하는 순환 알고리즘의 형태
- 전위 순회(Pre-order Traversals)를 포함한 다른 형태의 트리 순회는 모두 DFS의 한 종류
- 그래프 탐색의 경우 어떤 노드를 방문했었는지 여부를 반드시 검사해야 한다
  - 검사하지 않을 시 무한루프에 빠질 위험이 있다
- BFS에 비해 DFS의 구현이 비교적 간단
- 단순 검색 속도 자체는 BFS에 비해 느림

### DFS의 과정
1. 시작 노드(a)를 방문
   - 방문한 노드를 방문했다고 처리(방문 처리)
2. a와 인접한 노드들을 차례로 순회
   - 인접 노드가 없다면 종료
3. a와 이웃한 노드 b를 방문했다면, a와 인접한 노드를 방문하기 전에 b의 모든 이웃 노드들을 전부 방문
   - b를 시작 정점으로 하여 DFS를 다시 시작
4. b의 분기를 전부 완벽하게 탐색했다면 다시 a에 인접한 정점들 중 방문하지 않은 정점을 찾아 반복
   - b의 분기를 전부 완벽하게 탐색하지 못하면 a의 다른 이웃 노드를 방문할 수 없음
   - 방문 안된 정점이 없으면 종료
   - 방문 안한 정점이 있으면 해당 정점을 시작 정점으로 하여 DFS 다시 시작 

![DFS animation](https://github.com/Minho979/CS_Study/blob/main/contents/images/DFS-animation.gif)

<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/DFS-ex.png" width="600">

### DFS 구현 
구현 방법은 2가지로 나뉨
1. 재귀 호출 이용
2. 명시적인 스택 사용
   - 명시적인 스택을 사용하여 방문한 정점들을 스택에 저장하였다가 다시 꺼내어 작업

- 구현 이용된 그래프 상태

<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/DFS-and-BFS-graph-ex.png" width="500">

#### 재귀 호출을 이용한 DFS
```java
public class DFS {
	
	public static void recursionDFS(int[][] graph, int nodeIndex, boolean[] vistied) {
		
		// 방문 처리
		vistied[nodeIndex] = true;
		
		// 방문 노드 출력 
		System.out.print(nodeIndex + " >> ");
		
		// 방문한 노드의 인접 노드 찾기 
		for (int node : graph[nodeIndex]) {
			
			// 인접 노드가 방문한 적이 없다면 DFS 수행 
			if (!vistied[node]) {
				recursionDFS(graph, node, vistied);
			}
		}
		
	}
	
	public static void main(String[] args) {
		
		/* 
		 그래프의 연결 상태를 2차원 배열로 표현
		 인덱스가 각각의 노드번호가 될 수 있도록 0번 인덱스는 비어있는 상태 
		 1번 인덱스는 1번 노드를 뜻하고 노드의 배열의 값은 연결된 노드들  
		 */
		int[][] graph = {{}, {2, 3, 8}, {1, 6, 8}, {1, 5}, {5, 7}, {3, 4, 7}, {2}, {4, 5}, {1, 2}};
		
		// 방문 상태 확인을 위한 배열
		boolean[] vistied = new boolean[graph.length];
		
		System.out.print("재귀 호출 DFS 탐색 순서: ");
		recursionDFS(graph, 1, vistied);

	}

}
```

#### 스택을 활용한 DFS 
```java
import java.util.Stack;

public class DFS {

	public static void stackDFS(int[][] graph, int nodeIndex, boolean[] vistied) {
		
		// DFS에 사용할 스택 
		Stack<Integer> stack = new Stack<>();
		
		// 시작 노드를 스택에 삽입 
		stack.push(nodeIndex);
		
		// 시작 노드 방문 처리 
		vistied[nodeIndex] = true;
		
		// 스택이 비어있지 않은 경우 반복 
		while(!stack.isEmpty()) {
			
			// 스택에서 하나를 꺼내어 노드 인덱스 설정 
			nodeIndex = stack.pop();
			
			// 방문 노드 출력 
			System.out.print(nodeIndex + " >> ");
			
			// 꺼낸 노드와 인접한 노드 찾기 
			for (int LinkedNode : graph[nodeIndex]) {
				
				// 인접한 노드를 방문하지 않았을 경우 스택에 넣고 방문 처리 
				if (!vistied[LinkedNode]) {
					stack.push(LinkedNode);
					vistied[LinkedNode] = true;
				}
			}
		}
		
	}

	
	public static void main(String[] args) {
		
		/* 
		 그래프의 연결 상태를 2차원 배열로 표현
		 인덱스가 각각의 노드번호가 될 수 있도록 0번 인덱스는 비어있는 상태 
		 1번 인덱스는 1번 노드를 뜻하고 노드의 배열의 값은 연결된 노드들  
		 */
		int[][] graph = {{}, {2, 3, 8}, {1, 6, 8}, {1, 5}, {5, 7}, {3, 4, 7}, {2}, {4, 5}, {1, 2}};
		
		// 방문 상태 확인을 위한 배열
		boolean[] vistied = new boolean[graph.length];
		
		System.out.print("Stack DFS 탐색 순서: ");
		stackDFS(graph, 1, vistied);
	}

}
```

## 너비 우선 탐색(BFS, Breadth-First Search)
### 개념
- 루트 노드(혹은 임의의 다른 노드)에서 시작하여 인접한 노드를 먼저 탐색하는 방법
  - 시작 정점으로부터 가까운 정점을 먼저 방문하고 멀리 떨어져 있는 정점을 나중에 방문하는 순회 방법
  - 깊게(deep) 탐색하기 전에 넓게(wide) 탐색
  - 두 노드 사이의 최단 경로 혹은 임의의 경로를 찾고 싶을 때 사용
    - Ex) 한국에 있는 모든 경로를 그래프로 표현한 후 서울에서 부산까지의 경로를 찾는 경우
      - DFS: 모든 경로를 전부 다 살펴봐야할 수도 있음
      - BFS: 서울 또는 부산과 가까운 경로부터 탐색

### BFS의 특징
- 직관적이지 않은 면이 존재
  - 시작 노드에서 시작해서 거리에 따라 단계별로 탐색
- 재귀적으로 동작하지 않음
- 그래프 탐색의 경우 어떤 노드를 방문했었는지 여부를 반드시 검사해야 한다
  - 검사하지 않을 시 무한루프에 빠질 위험이 있다
- 방문한 노드를 차례로 저장한 후 꺼낼 수 있는 큐(Queue)를 사용
  - 선입선출(FIFO) 원칙으로 탐색
  - 일반적으로 큐를 이용하여 반복문으로 구현함
- '프림(Prim)', '다익스트라(Dijkstra)' 알고리즘과 유사

### BFS의 과정
1. 시작 노드를 방문 (방문한 노드 체크)
   - 큐에 방문한 노드를 삽입
   - 초기 상태의 큐는 시작 노드만이 저장
     - 시작 노드의 이웃 노드를 모두 방문한 다음 이웃의 이웃들을 방문
2. 큐에서 꺼낸 노드와 인접한 노드들을 차례로 방문
   - 큐에서 꺼낸 노드를 방문
   - 큐에서 꺼낸 노드와 인접한 노드들을 모두 방문
     - 인접한 노드가 없다면 큐의 앞에서 노드를 꺼냄
   - 큐에 방문한 노드를 삽입
3. 큐가 비워질 때까지 반복

![BFS animation](https://github.com/Minho979/CS_Study/blob/main/contents/images/BFS-animation.gif)

<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/BFS-ex.png" width="600">

### BFS 구현
- 구현 이용된 그래프 상태

<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/DFS-and-BFS-graph-ex.png" width="500">

#### 큐(Queue)를 이용한 BFS
``` java
import java.util.LinkedList;
import java.util.Queue;

public class BFS {

	public static String BFS(int[][] graph, int nodeIndex, boolean[] vistied) {
		
		// 탐색 순서 출력을 위함 
		StringBuilder sb = new StringBuilder();
		
		// BFS 탐색에 사용할 큐 
		Queue<Integer> queue = new LinkedList<Integer>();
		
		// 시작 노드를 큐에 추가 
		queue.offer(nodeIndex);
		
		// 시작 노드 방문 처리 
		vistied[nodeIndex] = true;
		
		// 큐가 빌 떄꺼자 반복 
		while(!queue.isEmpty()) {
			
			// 큐 값을 꺼내어 노드 인덱스로 설정  
			nodeIndex = queue.poll();
			
			// 방문 노드 출력 
			sb.append(nodeIndex + " >> ");
			
			// 큐에서 꺼낸 노드와 연결된 노드 확인 
			for (int i = 0; i < graph[nodeIndex].length; i++) {
				int temp = graph[nodeIndex][i];
				
				// temp 값이 방문하지 않은 노드라면 방문 처리 후 큐에 삽입 
				if(!vistied[temp]) {
					vistied[temp] = true;
					queue.offer(temp);
				}
			}
		}
		
		// 탐색 순서 리턴 
		return sb.toString();
		
	}

	public static void main(String[] args) {
		
		/* 
		 그래프의 연결 상태를 2차원 배열로 표현
		 인덱스가 각각의 노드번호가 될 수 있도록 0번 인덱스는 비어있는 상태
		 1번 인덱스는 1번 노드를 뜻하고 노드의 배열의 값은 연결된 노드들  
		 */
		int[][] graph = {{}, {2, 3, 8}, {1, 6, 8}, {1, 5}, {5, 7}, {3, 4, 7}, {2}, {4, 5}, {1, 2}};
		
		// 방문 상태 확인을 위한 배열
		boolean[] vistied = new boolean[graph.length];

		System.out.print("BFS 탐색 순서: " + BFS(graph, 1, vistied));
	}

}

```

## 깊이 우선 탐색(DFS)와 너비 우선 탐색(BFS) 비교
|DFS(깊이 우선 탐색)|BFS(너비 우선 탐색)|
|------------------|--------------------|
| 현재 정점에서 가장 깊게 갈 수 있는 점까지 들어가며 탐색 | 현재 정점에 연결된 가까운 점들부터 탐색 |
| 재귀함수 또는 스택으로 구현 | 큐를 이용하여 구현 |

### 시간 복잡도
- 모든 노드를 탐색하는 점에서 두 방식 모두 시간 복잡도는 동일하지만 검색 속도는 BFS가 더 빠름
- DFS와 BFS 모두 다음 노드가 방문한 노드인지 확인하는 시간과 각 노드를 방문하는 시간의 합
- 그래프의 구현 방식에 따라 시간 복잡도가 달라짐
  - 인접 리스트: $O(n+e)$ (n은 노드, e는 간선)
    - 간선의 정보만 저장되어 간선 존재 여부를 확인하기 위한 2중 for문이 요구되지 않음
  - 인접 행렬: $O(n^2)$ (n은 노드, e는 간선)
    - 간섭의 존재 유무를 확인하기 위한 2중 for문이 필요
  - 일반적으로 간선의 크기가 $n^2$보다 작아 인접 리스트가 효율적
 
### 활용하기 좋은 문제
- 단순히 그래프의 모든 정점을 방문하는 문제: DFS, BFS
- 경로의 특징을 저장하는 문제: DFS
  - BFS는 경로의 특징을 가지지 못함
- 최단거리를 구하는 문제: BFS
  - DFS는 처음 나오는 답이 최단거리가 아닐 수 있지만 BFS는 특성상 가장 먼저 구해지는 답이 최단거리
- 검색 대상 그래프가 큰 경우: DFS
- 검색 대상의 규모가 크지 않고, 검색 시작 지점으로부터 타겟이 멀지 않은 경우: BFS

> ⬆️:[Top](#깊이우선탐색DFS와-너비우선탐색BFS)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[알고리즘] 깊이 우선 탐색(DFS) 과 너비 우선 탐색(BFS)](https://devuna.tistory.com/32)
> - [[알고리즘] 깊이 우선 탐색(DFS)이란](https://gmlwjd9405.github.io/2018/08/14/algorithm-dfs.html)
> - [[알고리즘] 너비 우선 탐색(BFS)이란](https://gmlwjd9405.github.io/2018/08/15/algorithm-bfs.html)
> - [[Algorithm] DFS (Depth-first Search)를 Java로 구현해보자!](https://codingnojam.tistory.com/44)
> - [[Algorithm] BFS(Breadth-first search)를 Java로 구현해보자!](https://codingnojam.tistory.com/41)
