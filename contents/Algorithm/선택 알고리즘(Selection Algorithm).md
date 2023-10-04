# 선택 알고리즘(Selection Algorithm)
## 개념
- 입력값들 중 i번째로 작거나 큰 원소를 찾는 알고리즘
- 평균 선형시간 선택 알고리즘과 최악의 경우에도 선형시간을 보장하는 선택 알고리즘 두 가지가 있음

## 평균 선형시간 선택 알고리즘

### 원리
1. partition()을 호출해 찾고자하는 타겟의 인덱스를 리턴 받아 타겟의 위치 판별(왼쪽 배열, 오른쪽 배열)
  - 기준 원소의 인덱스를 p, 타겟의 인덱스가 i일 경우

    `p < i (타겟이 오른쪽 배열), p > i (타겟이 왼쪽 배열), p = i (타겟이 기준 원소인 경우)`   
2. 타겟이 속한 부분 배열을 판정하고 기준 원소가 타겟과 일치할 때까지 타겟이 속한 부분 배열에 대해 재귀적으로 수행

### 예시
pivot을 배열을 가장 끝 값으로 설정하는 경우의 예시 

- **pivot의 왼쪽 부분 배열을 탐색하는 경우**

	<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/SelectionAlgorithmEx1.jpeg" width="500">

	1\. pivot을 설정 (15)

	2\. 15를 기준으로 배열을 분할 

	3\. 분할된 배열 중 타겟 원소가 있는 부분 배열에서 pivot과 타겟이 일치할 때까지 재귀적으로 수행

- **pivot의 오른쪽 부분 배열을 탐색하는 경우**

	<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/SelectionAlgorithmEx2.jpeg" width="500">

	1\. pivot 설정(15)

	2\. 15를 기준으로 배열 분할

	3\. 분할된 배열 중 타겟 원소가 있는 부분 배열에서 pivot과 타겟이 일치할 때까지 재귀적으로 수행


### 시간 복잡도
- n개의 각 원소를 적어도 한번씩은 봐야하므로 $O(n)$
- $O(nlogn)$ 알고리즘으로 정렬 후 요구한 원소를 고르면 $O(nlogn)$
- $O(n)~O(nlogn)$의 범위 내에서 n에 근접하게 하는 문제가 있음
- 퀵 정렬의 partition()을 이용하기에 최악의 경우 $O(n^2)$
  - 분할의 영향을 받음
- 평균적으로는 $O(n)$ 최악의 경우 $O(n^2)$
  - 평균 수행시간을 점화식으로 나타낼 경우 $T(n) <= max(T(k-1), T(n-k))+O(n)$으로 추정 후 증명법으로 $T(n) = O(n)$임을 알 수 있음
  - 최악의 경우 수행시간의 경우 $T(n) = T(n-1) + O(n)$으로 $T(n) = O(n^2)$

### 구현 코드
```java
public class Selection {
	
	public static int selection(int[] a, int begin, int end, int i) {
		if (begin == end) { // a의 원소가 하나뿐인 경우 
			return a[begin];
		}
		
		int pivot = partition(a, begin, end); // 기준 원소 설정 
		
		// 기준 원소 a[pivot]이 범위 내에서 k번째로 작은 원소임을 의미 
		int k = pivot - begin +1; 
		
		// 찾는 원소가 왼쪽 부분 배열에 있는 경우 
		if (i < k) {
			return selection(a, begin, pivot -1, i); 
		}
		// 찾는 원소가 기준 원소인 경우 
		else if(i == k) {
			return a[pivot];
		}
		// 찾는 원소가 오른쪽 부분 배열에 있는 경우 
		else {
			return selection(a, pivot +1, end, i-k);
		}
	}
	
	// 부분 배열의 가장 끝 요소를 피벗으로 삼는 분할 
	private static int partition(int[] a, int begin, int end) {		
		int left = begin;	    // 왼쪽 시작점
		int right = end;        // 오른쪽 시작점
		int pivot = a[end];		// 부분배열의 오른쪽 요소를 피벗으로 설정
		
		// left가 right보다 작을 때 까지만 반복
		while(left < right) {
			
			/*
			 right가 left보다 크면서, left의 요소가 
			 pivot보다 큰 원소를 찾을 떄 까지 left를 증가
			 */
			while(a[left] < pivot && left < right) {
				left++;
			}
			
			/*
			 right가 left보다 크면서, right의 요소가 
			 pivot보다 작거나 같은 원소를 찾을 떄 까지 right를 감소
			 */
			while(a[right] >= pivot && left < right) {
				right--;
			}
			
			// 교환 될 두 요소를 교환 
			swap(a, left, right);
		}
	
		/*
		 마지막으로 맨 처음 pivot으로 설정했던 
		 a[right]의 원소와 right가 가리키는 원소를 바꾼다.
		 */
		swap(a, end, right);
		
		// 두 요소가 교환되었다면 피벗이었던 요소는 right에 위치하므로 right를 반환한다.
		return right;
	}
	
	public static void swap(int[] a, int i, int j) {
		int temp = a[i];
		a[i] = a[j];
		a[j]= temp;
		
	}

}
```

## 최악의 경우 선형시간 선택 알고리즘(Linear Select)
선택 알고리즘이 분할의 균형에 영향을 받는 것을 줄이기 위해 분할 균형이 어느정도 보장되도록 하는 선택 알고리즘

단, 분할의 균형을 유지하기 위한 오버헤드가 지나치게 클 경우 의미가 퇴색되므로 주의가 필요

### 원리 
1. 원소의 총 개수가 5개 이하이면 원하는 원소를 찾고 알고리즘 종료
2. 전체 원소를 5개씩의 원소를 가진 n/5개의 그룹으로 분할
   - 이때, 꼭 5개의 원소로 나누지 않아도 된디. 3개의 원소로 나눌 경우 n/3개의 그룹으로 분할
3. 각 그룹에서 중앙값을 찾는다.
   - 이때 중앙값들을 m1, m2, ..., m(n/5)로 설정
4. m1, m2, ..., m(n/5)들의 중앙값 M을 재귀적으로 구한다.
   - mk의 값들이 홀수개면 중앙값이 하나이지만 짝수개인 경우 두 중앙값 중 임의로 하나를 선택
5. M을 기준 원소로 삼아 전체 원소를 분할
6. 분할된 두 그룹 중 적합한 쪽에서 1-6단계를 재귀적으로 반복

### 예시

### 시간 복잡도

### 구현 코드


> ⬆️:[Top](#선택-알고리즘Selection-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
