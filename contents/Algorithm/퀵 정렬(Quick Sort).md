# 퀵 정렬(Quick Sort)
## 개념

  ![Quick Sort](https://github.com/Minho979/CS_Study/blob/main/contents/images/QuickSort.gif)

  - 하나의 리스트를 피벗(pivot)을 중심으로 두 개의 비균등한 크기로 분할하고 분할된 부분 리스트를 정렬한 후 두 리스트를 병합하여 정렬
    - 피벗(pivot): 리스트 안에 있는 원소 중 선택한 하나의 원소, 중앙 값에 가까운 값일 수록 성능 향
    - 분할 정복(Divide and Conquer) 알고리즘: 문제를 분할하여 각각 해결한 다음 병합을 통해 원래의 문제 해결, 재귀호출을 이용하여 구현
  - 한쪽으로 치우치지만 않으면 평균적으로 매우 빠른 수행 속도를 보임
  - 불안정 정렬(Unstable sort)
  - 다른 원소와 비교만을 통해 정렬을 수행하는 '비교 정렬'

## 퀵 정렬의 과정
  - 분할(Divide): 피벗을 기준으로 비균등하게 2개의 부분 배열로 분할
    - 왼쪽: 피벗보다 작은 요소, 오른쪽: 피벗보다 큰 요소
  - 정복(Conquer): 부분 배열을 정렬. 부분 배열읠 크기가 충분히 작지 않으면 재귀 호출을 이용하여 다시 분할 정복 과정을 반복
  - 결합(Combine): 정렬된 부분 배열을 하나의 배열에 병
  - 순환 호출이 한번 진행될 때마다 최소 피벗 하나는 최종적으로 위치가 정해지므로 해당 알고리즘의 종료를 보장
  1. 리스트 안에 있는 한 원소(피벗)를 선택
  2. 피벗보다 작은 값들은 피벗의 왼쪽으로 이동하고, 큰 값은 오른쪽으로 이동
  3. 피벗을 제외한 왼쪽 리스트와 오른쪽 리스트를 다시 정렬
     - 부분 리스트에 대해 재귀 호출을 이용하여 정렬 반복
     - 부분 리스트 내에서 다시 피벗을 정하고 2개의 부분 리스트로 나누는 과정을 반복
  4. 부분 리스트들이 더 이상 분할이 불가능 할 때까지 반복
     - 리스트의 크기가 0이나 1이 될 때까지 반복

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/QuickSort.png" width="500">

## 시간 복잡도
  - **최선의 경우(균등하게 나뉘어지는 경우)** 
    
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/QuickSortTimeComplexity-Best.png" width="630">
    
    - 비교 횟수: 재귀 호출의 깊이(단계 수) * 각 순환 호출 단계의 비교 연산
      - 깊이: 레코드 개수 n이 2의 거듭 제곱$(n=2^k)$일 경우  $k=logn$
      - 비교: 전체 리스트의 대부분의 레코드를 비교하므로 평균 $n$
      - $nlogn$
    - 이동 횟수: 비교 횟수보다 적으므로 무시할 수 있음
    - $O(nlogn)$

  - **최악의 경우(불균형하게 나누어지는 경우, 이미 정렬된 리스트에 대해 퀼 정렬을 하는 경우)**
    
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/QuickSortTimeComplexity-Worst.png" width="500">

    - 비교 횟수: 재귀 호출의 깊이(단계 수) * 각 순환 호출 단계의 비교 연산
      - 깊이: $n$, 비교: $n$
      - $n^2$
    - 이동 횟수: 비교 횟수보다 적으므로 무시할 수 있음
    - $O(n^2)$

  - 평균적인 경우 $O(nlogn)$

## 공간 복잡도
  - 배열 안에서 교환하기에 $O(n)$
  - 재귀호출 공간 $O(logn)$
 
## 특징
  - 상대적으로 작은 메모리만을 사용하기에 제자리 정렬(in-place) 정렬이라고 기술하기도 함
    - 공간 복잡도 $O(n), O(logn)$
  - 최악의 경우를 제외하고 매우 빠른 수행 속도를 보임
    - 최악의 경우: 피벗이 한쪽으로 치우친 경우
  - 중복된 키 값의 위치가 정렬 과정에서 바뀔 수 있으므로 불안정 정렬(Unstable sort)
  - 시간 복잡도가 $O(nlogn)$으로 동일한 다른 정렬 알고리즘과 비교했을 때 가장 빠름
    - 불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환하며, 한번 결정된 피벗들이 이후 연산에서 제외되는 특성때문

## 장점
  - 속도가 빠르다
    - 시간 복잡도가 O(nlogn)를 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠른 속도
  - 추가적인 메모리 공간을 필요로 하지 않음
    - 재귀 호출의 깊이에 따라 $O(logn)$의 메모리를 필요로 함

## 단점
  - 정렬된 리스트에 대해 퀼 정렬의 불균형 분할에 의해 수행시간이 $O(n^2)$으로 버블 정렬과 다를 것 없는 성능을 보임
    - 이를 방지하기위해 피벗을 선택할 때 균등하게 분할할 수 있는 데이터를 선택

## 구현 코드
``` java
public class QuickSort {
	
	public static void quickSort(int a[], int begin, int end) {
		
		if (begin < end) {
			int p = partition(a, begin, end); // 분할
			quickSort(a, begin, p); 	  // 왼쪽 정렬
			quickSort(a, p+1, end); 	  // 오른쪽 정렬
		}
	}
	
	public static int partition(int a[], int begin, int end) {
		int left = begin -1;	      // 왼쪽의 끝에서 1 벗어난 위치 (왼쪽 시작점)
		int right = end +1;	      // 오른쪽의 끝에서 1 벗어난 위치 (오른쪽 시작점)
		int pivot = a[(begin+end)/2]; // 부분 리스트의 중간 원소를 피벗으로 설정
		
		while(true) {
			/*
			left를 1 증가 시키고 left의 위치 원소가 피벗보다 큰 원소를 찾을 때까지 반복
			*/
			do {
				left++;
			} while(a[left] < pivot);

			/*
			right를 1 감소한 뒤의 right의 위치가 left보다 크거나 같은 위치이면서
			right의 요소가 피벗보다 작은 원소를 찾을 때까지 반복
			*/
			do {
				right--;
			} while(a[right] > pivot && lo <= hi);

			// left가 right보다 크다면 서로 엇갈린 것이므로 swap하지 않고 right를 리턴 
			if(left >= right) {
				return right;
			}

			// 교환할 두 요소를 서로 교환 
			swap(a, left, right);
		}
		
	}

	public static void swap(int a[], int i, int j) {
		int temp = a[i];
		a[i] = a[j];
		a[j] = temp;
	}

}
```

> ⬆️:[Top](#퀵-정렬Quick-Sort)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)
> - [[알고리즘] 퀵 정렬(quick sort)이란](https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html)
> - [자바 [JAVA] - 퀵 정렬 (Quick Sort)](https://st-lab.tistory.com/250)
