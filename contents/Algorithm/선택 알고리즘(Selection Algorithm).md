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
    - $max(T(k-1), T(n-k))+O(n)$: 분할된 양쪽 중 큰 쪽을 처리하는 비용의 평균
    - $O(n)$: 재귀호출을 제외한 오버헤드 (분할이 대부분)
  - 최악의 경우 수행시간의 경우 $T(n) = T(n-1) + O(n)$으로 $T(n) = O(n^2)$
    - $T(n-1)$: 분할이 $0:n-1$로 되고 큰쪽을 처리하는 비용 (문제의 크기가 1씩 작아짐)
    - $O(n)$: 재귀호출을 제외한 오버헤드 (분할이 대부분)

### 구현 코드
```java
package select;

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

<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/linearSelectPartition.jpeg" width="600">

### 원리 
1. 원소의 총 개수가 5개 이하이면 원하는 원소를 찾고 알고리즘 종료
2. 전체 원소를 5개씩의 원소를 가진 $⌈n/5⌉$개의 그룹으로 분할
   - 이때, 꼭 5개의 원소로 나누지 않아도 된디. 3개의 원소로 나눌 경우 n/3개의 그룹으로 분할
3. 각 그룹에서 중앙값을 찾는다.
   - 이때 중앙값들을 $m_1, m_2, ..., m_{⌈n/5⌉}$로 설정
4. $m_1, m_2, ..., m_{⌈n/5⌉}$들의 중앙값 M을 재귀적으로 구한다. `call linearSelect`
   - $m_k$의 값들이 홀수개면 중앙값이 하나이지만 짝수개인 경우 두 중앙값 중 임의로 하나를 선택
   - ex. $m_k$가 15개인 경우 재귀호출하여 8번째 작은 $m_k$를 찾고 이를 M으로 설정
5. M을 기준 원소로 삼아 전체 원소를 분할
6. 분할된 두 그룹 중 적합한 쪽에서 1-6단계를 재귀적으로 반복 `call linearSelect`


### 예시

<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/linearSelectEx.jpeg" width="500">

1. 주어진 배열을 5개의 원소를 가진 배열로 분할
2. 분할된 배열의 중앙값을 연산하여 중앙값들이 모인 배열을 생성
3. 중앙값 배열에서 M이라는 중앙값들의 중앙값을 산출
4. M을 기준으로 배열을 분할
5. 타겟 원소를 포함하여 원소 개수가 5이하인 배열이 산출될 때까지 재귀적으로 위의 과정을 반복
6. 원소 수가 5개 이하가 되었다면 타겟 원소를 찾고 알고리즘 종료

### 시간 복잡도
- 분할 균형을 유지하게 되면서 partition()의 시간복잡도를 $O(nlogn)$으로 낮아짐
  - 분할의 균형을 유지하기 위한 전처리 단계가 추가되었지만 지나치게 크지만 않으면 됨
  - 분할의 균형을 맞춤으로써 분할 균형의 영향을 낮춤
- 그 외의 경우 평균 선형시간 선택 알고리즘과 동일
- 평균, 최악의 경우 $O(n)$
  - 점화식으로 표현할 경우 $T(n) <= T(⌈n/5⌉) + T(7n/10 +2) + O(n)$으로 추정 후 증명법으로 $T(n) = O(n)$임을 알 수 있음
    - $T(⌈n/5⌉)$: 4단계
    - $T(7n/10 +2)$: 6단계
    - $O(n)$: 1, 2, 3, 5단계



### 구현 코드
```java
package select;

import static select.Selection.selection;

public class LinearSelect {
	
	// 배열 a에서 idx번쨰로 작은 값 찾기 
	public static int linearSelect(int[] a, int size, int target) {
		// 배열 분할(크기 설정)
		int midArrCount = (size / 5) +1;
		
		// 중간 값 배열을 분할된 배열의 개수만큼의 크기로 생성 
		int [] midArr = new int[midArrCount];
		
		int result = linearSelect(a, midArr, 0, size-1, target);
		
		return result;
		
	}
	
	public static int linearSelect(int[] a, int[] midArr, int start, int end, int target) {
		// 원소 수 5개 이하인 경우 target을 찾음 
		if (start - end < 5) {
			return selection(a, start, end, target);
		}
		
		// 기준 원소 설정 
		int pivot = partition(a, start, end, getMidValue(a, midArr, start, end));
		
		// 기준 원소 a[pivot]이 범위 내에서 k번째로 작은 원소임을 의미
		int k = pivot - start +1;
		
		// 찾는 원소가 왼쪽 부분 배열에 있는 경우 
		if (target < k) {
			return linearSelect(a, midArr, start, pivot -1, target);
		}
		
		// 찾는 원소가 기준 원소인 경우 
		else if(target == k) {
			return a[pivot];
		}
		
		// 찾는 원소가 오른쪽 부분 배열에 있는 경우 
		else {
			return linearSelect(a, midArr, pivot +1, end, target);
		}
	}
	
	// 중간 값을 찾아 반환 
	public static int getMidValue(int[] a, int[] midArr, int start, int end) {
		int midIdx = 0;
		int [] midTempArr = new int [5];
		
		for (int i = start; i <= end;) {
			int j = 0;
			for (; j < 5 && i <= end; j++, i++) {
				midTempArr[i] = a[i];
			}
			midArr[midIdx++] = selection(midTempArr, 0, j -1, 3);
		}
		
		return selection(midTempArr, 0, midIdx -1, midIdx/2);
	}
	
	
	// 배열의 끝 값을 기준으로 분할 
	private static int partition(int[] a, int start, int end, int midValue) {
		int i = start;
		int j = start;
		int midValueIdx = start;
		
		while (i < end && j < end) {
			if (a[j] == midValue) {
				midValueIdx = j++;
				continue;
			}
			if (a[j++] < midValue) {
				swap(a, i, j-1);
				i++;
			}
		}
		swap(a, i, midValueIdx);
		return i;
	}
		
	public static void swap(int[] a, int i, int j) {
		int temp = a[i];
		a[i] = a[j];
		a[j]= temp;
		
	}
	
	public static void main(String[] args) {
		int  a[] = {5, 6, 3, 2, 1, 4, 7, 9, 8, 10, 13, 12, 11, 14, 15};
		int size = a.length;
		int target = linearSelect(a, size , 6);
		
		System.out.print(target);

	}

}

```

> ⬆️:[Top](#선택-알고리즘Selection-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
