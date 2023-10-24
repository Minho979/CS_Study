# 그리디 알고리즘(Greedy Algorithm)
## 개념
- 선택의 순간마다 당장 눈앞의 최적의 상황만을 추구하여 최종적인 답을 도출하는 알고리즘
- 순간마다 하는 선택은 해당 순간에 지역적으로 최적인 선택을 통해 최종(전역적) 해답을 도출을 하더라도, 그것이 최적해라는 보장이 없다.
  - 드믈게 최적해가 보장되는 경우도 있다.
- 지역적으로 최적이면서 전역적으로 최적인 문제에 대해 적용이 가능하다.
- 최적해를 찾을 수 있다면 찾고, 그것이 어렵다면 시간 내에 최적에 근사한 답을 찾는 것을 목표로 한다.
  - 탐욕 알고리즘은 근사 알고리즘으로 이용이 가능하다.
  - 근사 알고리즘(Approximation Algorithm): 최적화된 답을 구할 수는 없지만, 비교적 빠른 시간 내에 어느정도 보장된 근사해를 구하는 알고리즘


## 그리디 알고리즘의 해결 과정
1. 선택 절차(Selection Procedure): 현재 상태에서의 최적의 해답을 선택
2. 적절성 검사(Feasibility Check): 선택된 해가 문제의 조건을 만족하는지 검사
3. 해답 검사(Solution Check): 문제가 해결되었는지 검사하고, 해결되지 않았다면 1번 과정부터 반복

## 적용 조건
1. 탐욕적 선택 속성(Greedy Choice Property): 이전의 선택이 이후의 선택에 영향을 주지 않는다.
2. 최적 부분 구조(Optimal Substructure): 최종 최적해가 부분 문제에 대한 최적해로 구성된다.

- 위의 두 가지 조건을 미충족하는 경우 그리디 알고리즘은 최적해를 보장하지 못한다.
  - 이러한 경우에도 빠른 연산 속도를 바탕으로 근사 알고리즘으로 사용할 수 있다.
  - 근사해를 구할 수 있는지를 보장하기 위해서는 엄밀한 증명이 필요하다.
- 매트로이드 구조가 있는 문제에 대해서 그리디 알고리즘은 언제나 최적해를 보장한다.
  - 매트로이드: 부분집합들의 집합으로 어떤 성질을 만족하는 수학적 구조를 갖고 있다.

## 그리디 알고리즘으로 최적해가 보장되지 않는 예
### 이진 트리의 최적합 경로 찾기
- 각 노드에 양 가중치가 할당된 이진 트리
  - 노드의 가중치는 미리 알 수 없고, 어떤 노드에 이르면 그 노드의 자식 노드 가중치를 알 수 있다.
  - 루트부터 시작해 왼쪽/오른쪽 분기할 방향을 매단계 결정
  - 각 경로의 점수는 루트 노드에서 리프 노드에 이를때까지 만난 노드의 가중치의 합
- 문제: 경로의 점수를 최대화하는 경로를 찾아라

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Greedy-BinaryTree.png' width='500'>

  - 최적해: 빨간 경로
  - 그리디: 파란 경로 

### 동전 바꾸기
- 동전을 모아 특정 액수를 만들되 동전의 개수를 최소로 하라.
- 모든 동전의 액면이 바로 아래 액면의 배수가 되는 경우 그리디 알고리즘으로 최적해가 보장된다.
  - 예) 500원, 100원, 50원, 10원, 5원, 1원으로 3256원 만들기
    - 500원 6개, 100원 2개, 50원 1개, 5원 1개, 1원 1개
    - 총 11개로 최적해를 보장한다.
- 바로 아래 액면의 배수가 아닌 경우 최적해를 보장하지 않는다.
  - 예) 500원, 400원, 100원, 75원, 50원으로 1300원 만들기
    - 그리디: 500원 2개, 100원 3개
    - 최적해: 500원 1개, 400원 2개
    - 그리디의 답은 5개인 반면 최적해는 3개로 최적해와 차이가 발생

### 보따리 문제(0/1 Knapsack Problem)
- 문제: 영량이 정해진 보따리에 가치와 부피가 제 각각인 물건들을 넣되, 넣은 물건의 총 가치가 최대가 되도록 하라.
  - 보따리의 용량 21L
  - A: (250원, 10L) B: (450원, 15L), C: (270원, 10L)
  - 그리디: 보따리에 B 1개를 넣음 -> 총 가치 450원
  - 최적해: 보따리에 A, C를 넣음 -> 총 가치 520원
- 그리디 알고리즘은 해당 문제에 용량이 초과되지 않는 선에서 단위 부피 당 가치가 큰 물건부터 보따리에 넣는다. 따라서 그리디 알고리즘은 최적해를 보장하지 못한다.
  하지만 물건을 자를 수 있다면 (Fractional Knapsack Problem) 방식으로 최적해를 보장할 수 있다.

## 그리디 알고리즘으로 최적해가 보장되는 예
### 최소 신장 트리
- [Prim 알고리즘](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/Prim%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md)
- [Kruskal 알고리즘](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/Kruskal%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md)
### 최단 경로
- [다익스트라(Dijkstra) 알고리즘](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EB%8B%A4%EC%9D%B5%EC%8A%A4%ED%8A%B8%EB%9D%BC(Dijkstra)%20%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98.md)
### 회의실 배정 문제
- 문제: 1개의 회의실에 여러 사람이 회의 시작 시간과 종료시간을 명시해서 회의실 사용을 신청한다. 겹치는 시간이 없게 가장 많은 수의 회의를 소화하도록 사용 스케줄을 정하라.
- 그리디한 아이디어
  - 소요 시간이 가장 짧은 회의순 배정
  - 소요 시간이 가장 이른 회의순 배정
  - 종료 시간이 가장 이른 회의순 배정 (이것만이 최적해를 보장한다.)
- 예시) 8개의 회의 신청(시작 시간, 종료 시간)
  - (3, 5), (1, 6), (6, 7), (5, 9), (8, 13), (7, 14), (12, 18), (16, 20)
  - 종료 시간 순 정렬후 앞에서부터 겹치지 않게 선택
  - (3, 5), (6, 7), (8, 13), (16, 20)이 최적해가 된다. 

``` java
public class Main {

	public static void main(String[] args) {

		Scanner sc = new Scanner(System.in);

		int n = sc.nextInt();

		Reservation[] list = new Reservation[n]; // 객체 생성

		for (int i = 0; i < list.length; i++) {
			int startTime = sc.nextInt();
			int endTime = sc.nextInt();

			list[i] = new Reservation(startTime, endTime); // 입력받아 대입
		}

		Arrays.sort(list); // 정렬

		int cnt = 1; // 최소 1개 이상 예약이 되므로 1
		int endTime = list[0].getEndTime(); // 초기값 설정
		for (int i = 1; i < n; i++) { // 첫 값 [0]은 비교군이므로 1부터 시작
			if(list[i].getStartTime() >= endTime) { // endTime보다 크면 예약 가능
				cnt++;
				endTime = list[i].getEndTime(); // endTime의 값 갱신
			}
		}

		System.out.println(cnt);

		sc.close();

	}

}

class Reservation implements Comparable<Reservation> {
	private int startTime; // 시작 시간
	private int endTime; // 종료 시간

	public Reservation(int startTime, int endTime) {
		this.startTime = startTime;
		this.endTime = endTime;
	}

	// getter
	public int getStartTime() {
		return startTime;
	}


	public int getEndTime() {
		return endTime;
	}

	@Override
	public int compareTo(Reservation o) {
		if (this.endTime > o.endTime) { // 끝나는 시간 기준 오름차순 정렬
			return 1;
		}
		else if (this.endTime < o.endTime) {
			return -1;
		}
		else // 끝나는 시간이 같을 때 시작 시간 기준 오름차순 정렬
			return this.startTime - o.startTime;
	}

}

```

> ⬆️:[Top](#그리디-알고리즘Greedy-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[알고리즘] 탐욕 알고리즘(Greedy Algorithm)](https://hanamon.kr/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%ED%83%90%EC%9A%95%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-greedy-algorithm/)
