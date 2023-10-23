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
- 예시에 이용된 그래프
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/SCC-Graph.png' width='500'>

1. 정점 1부터 DFS를 수행하여 순서대로 방문하고 스택에 삽입
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/SCC-Ex1.png' width='500'>

- LIFO를 통해 8에서 부모 노드로 이동할 수 있는지 확인
- 4로 이동할 수 있으므로 SCC 해당 X 

2. 정점 4에서 부모 노드로 이동할 수 있는지 확인
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/SCC-Ex2.png' width='500'>

- 3으로 이동할 수 있으므로 SCC 해당 X

3. 정점 3에서 부모 노드로 이동할 수 있는지 확인
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/SCC-Ex3.png' width='500'>

- 7으로 이동할 수 있으며 새로운 정점 7을 방문하고 스택에 삽입
- 7에서 6으로 이동하고 스택에 삽입 

4. 정점 6에서 부모 노드로 이동할 수 있는지 확인
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/SCC-Ex4.png' width='500'>

- 7로 이동하고 7은 부모 노드로 이동할 수 없으므로 SCC에 해당
- 정점 7과 그 위에 쌓여있는 6을 하나로 묶어 하나의 SCC 성립

5. 정점 3에 대해 부모 노드로 이동할 수 있는지 확인 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/SCC-Ex5.png' width='500'>

- 7로 이동할 수 있지만 7은 이미 다른 SCC로 빠져나갔기에 정점 3과는 다른 SCC에 해당
- 동일 SCC내에서는 이동할 수 있는 부모 노드가 없어 3위에 쌓여있는 정점들을 하나로 묶어 하나의 SCC 성립

6. 정점 2로 돌아가 방문하지 않았던 노드 5를 방문하고 스택에 삽입
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/SCC-Ex6.png' width='500'>

- 5에 대해 부모 노드로 이동할 수 있는지 확인하고 1로 이동할 수 있으므로 1로 이동

7. 정점 1은 루트 노드이기에 더이상 방문 할 수 있는 노드가 없음
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/SCC-Ex7.png' width='500'>

- 정점 1위의 모든 정점을 하나로 묶어 하나의 SCC 구성

8. 모든 SCC를 발견하여 스택이 비었으므로 종료
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/SCC-Ex8.png' width='500'>

- [6, 7], [3, 4 ,8], [1, 2, 5]라는 강연결 요소 발견


## 시간 복잡도
- 모든 정점을 탐색하고 간선의 개수만큼 추가 탐색하므로 $O(|V|+|E|)$ 

## 구현 코드
``` java
public class SCC_Algorithm {

	static int MAX = 10001;
	static int v, e, id;
	static int[] d = new int[MAX];
	static int sccNum; // scc 개수
	static int[] sn = new int[MAX]; // i가 속한 SCC의 번호
	static List<List<Integer>> a = new ArrayList<>();
	static boolean[] finished = new boolean[MAX]; // SCC 성립되면 true
	static Stack<Integer> s = new Stack<>();
	static List<List<Integer>> SCC = new ArrayList<>();
	
	public static void main(String[] args) throws Exception {

		// 그래프 정보 입력
		BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
		StringTokenizer st = new StringTokenizer(br.readLine());
		int n = Integer.parseInt(st.nextToken());	// 정점 수 
		int c = Integer.parseInt(st.nextToken());	// 간선 수 
	        for(int i = 0; i<MAX; i++){
	            List<Integer> list = new ArrayList<>();
	            a.add(list);
	        }
	        for(int i = 0; i<c; i++){
		        st = new StringTokenizer(br.readLine());
	            int x = Integer.parseInt(st.nextToken());	// 출발 정점 
	            int y = Integer.parseInt(st.nextToken());	// 도착 정점 
	
	            a.get(x).add(y);
	        }

		// DFS를 수행하며 SCC 추출
		for (int i = 1; i <= n; i++) {
			if (d[i] == 0) DFS(i);
		}

		// sccNum = SCC 개수
		System.out.println("SCC 개수 : "+sccNum);

		// 각 SCC 출력
		for (List<Integer> currSCC : SCC) {
			for (int curr : currSCC){
				System.out.print(curr+" ");
			}
			System.out.println();
		}
	}

	public static int DFS(int c){
		d[c] = ++id;
		s.push(c);
		
		int result = d[c];
	        Iterator<Integer> itr = a.get(c).iterator();
		while(itr.hasNext()){
            	int next = itr.next();

			// 처음 방문하는 정점
			if(d[next] == 0) result = Math.min(result, DFS(next));

			// 방문은 했었지만 SCC 성립 전인 정점
			else if(!finished[next]) result = Math.min(result, d[next]);
		}
		
		if(result == d[c]){
			List<Integer> scc = new ArrayList<>();
			while(true){
				int t = s.pop();
				scc.add(t);
				finished[t] = true;
				sn[t] = sccNum;
				if(t == c) break;
			}
			SCC.add(scc);

			sccNum++;
		}
		return result;
	}
}
```
```java
입력 값
8 11   // 정점 수, 간선 수 
1 2    // 출발 정점, 도착 정점
2 3
2 5
3 4
3 7
4 3
4 8
5 1
6 7
7 6
8 4

출력 값
SCC 개수 : 3
6 7 
8 4 3 
5 2 1 
```


   
> ⬆️:[Top](#강연결-요소Strongly-Connected-Component)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[알고리즘] 강한 연결 요소 추출 알고리즘 (Strongly Connected Component)](https://yjg-lab.tistory.com/188)
> - [강한 연결 요소 추출 알고리즘 (Strongly Connected Component)](https://velog.io/@gkdis6/알고리즘-강한-연결-요소-추출-알고리즘-Strongly-Connected-Component)
