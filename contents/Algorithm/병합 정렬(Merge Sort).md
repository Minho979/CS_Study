# 병합 정렬(Merge Sort)
## 개념

  ![MergeSort](https://github.com/Minho979/CS_Study/blob/main/contents/images/MergeSort.gif)

  - 하나의 리스트를 균등한 크기로 분할하고, 분할된 부분 리스트들을 독립적으로 정렬한 후 정렬된 부분 리스트를 합하여 전체 리스트 정렬함
    - 분할 정복(Divide and Conquer) 알고리즘 기반
  - 데이터를 비교하면서 찾기 때문에 비교 정렬
  - 추가적인 공간이 필요하기에 제자리 정렬(in-place sort)이 아님
  - 최대한 잘게 쪼개어 앞부분의 리스트부터 합치기 때문에 안정정렬(Stable Sort) 알고리즘
  - n개의 부분 리스트로 분할하는 방법(n-way)과 2개의 부분 리스트로 분할하는 (2-way)방법이 존재
    - 하향식 2-way 합병 정렬을 자주 사용 

## 병합 정렬의 과정
  - 분할(Divide): 입력 배열을 같은 크기의 2개의 부분 배열로 분할
  - 정복(Conquer): 부분 배열을 정렬, 부분 배열의 크기가 충분히 작지 않으면 재귀 호출을 이용해 다시 분할 정복 방법을 적용
    - 분할된 부분 배열의 크기가 1이 아닌 경우 분할과정부터 다시 수행
  - 결합(Combine): 정렬된 부분 배열들을 하나의 배열에 병합
  1. 2개의 리스트 값들을 처음부터 하나씩 비교하여 더 작은 값을 보조 리스트에 이동
  2. 둘 중 하나가 끝날 때까지 반복
  3. 두 개의 리스트 중 하나의 리스트가 먼저 끝날 경우 나머지 리스트의 값을 전부 보조 리스트에 복사
  4. 4. 보조 리스트의 값을 기존의 리스트로 복사

### 예시
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/MergeSort.png" width="630">
  
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/MergeSortCombine.png" width="630">
 	
   - 부분 리스트의 처음 값 부터 비교하여 정렬하기에 안정 정렬(Stable Sort)가 보장

## 시간 복잡도

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/MergeSort-TimeComplexity.png" width="630">

  - 각 부분 배열을 정렬하는 시간과 병합 시간의 곱
	  - 합병 단계의 비교 연산
	    - 크기가 n/2, n/4, ..., 1인 배열을 비교하므로 최대 n번
	  - 재귀 호출의 깊이(병합 단계 수)
	    - $n=2^k$인 경우, $k = logn$
	  - $n * log n = nlogn$
  - 병합 단계에서 이동 횟수 또한 영향을 미침
    - 재귀 호출의 깊이 ($log n$)
    - 이동 연산($2n$): 임시 배열에 복사했다가 다시 가져옴
    - $2n * log n = 2nlogn$
  - $2nlogn + nlogn= O(nlogn)$
  - 최악, 평균, 최선 모두 $O(nlog n)$

## 공간 복잡도
  - 보조 리스트를 이용하여 정렬하므로 $O(n)$
 
## 특징
  - 추가적인 리스트(공간)이 필요
  - 각 부분 배열을 정렬할 때도 병합 정렬을 재귀적으로 호출하여 적용
  - 2개의 리스트를 병합(merge)하는 단계에서만 실제로 정렬이 이루어짐

## 장점
  - 안정 정렬(Stable Sort)
  - 항상 부분 리스트로 쪼개어 작동하기에 데이터의 크기와 관계없이 항상 $O(nlogn)$ 보장하기에 안정적
  - 레코드를 연결 리스트로 구현할 시 데이터의 이동 시간이 매우 작아져 큰 레코드 정렬 시 효율적
    - 연결 리스트로 구현할 시 링크 인덱스 값만 변경되며 제자리 정렬(in-place sort)로 구현 가능
## 단점
  - 제자리 정렬(in-place sort)가 아니기에 추가 메모리 공간 $O(n)$이 필요
  - 정렬된 원소들을 본 리스트로 복사하는 과정이 많은 시간이 소요
    - 레코드들의 크기가 큰 경우 이동 횟수가 많아지기에 시간 낭비가 증가

## 구현 코드
``` java
public class MergeSort {
	
	public static void mergeSort(int[] a, int left, int right) {
		if (left < right) {
			int mid  = (left + right) / 2; // 반으로 나누기 위한 변수 값 
			mergeSort(a, left, mid);       // 왼쪽 부분 리스트 분할 재귀 호출
			mergeSort(a, mid+1, right);    // 오른쪽 부분 리스트 분할 재귀 호출
			merge(a, left, mid, right);    // 원소를 Merge
			
		}
	}
	
	public static void merge(int[] a, int left, int mid, int right) {
		int lp = left;  // 왼쪽 시작 인덱스 
		int rp = mid+1; // 오른쪽 시작 인덱스 
		int idx = left; // 임시 배열 시작 인덱스 
		
		int[] temp = new int [a.length];
		
		// 둘 중 하나의 배열이 빌 때까지 반복 
		while (lp <= mid && rp <= right) {
			// 왼쪽이 작거나 같을 때 idx에 lp값 삽입 후 lp 값, idx ++
			if (a[lp] <= a[rp]) {
				temp[idx] = a[lp];
				lp++;
			}
			// 오른쪽이 작을 때 idx에 rp 값 삽입 후 rp 값, idx ++
			else {
				temp[idx] = a[rp];
				rp++;
			}
			idx++;
		}
		
		// 왼쪽 배열에 원소가 남아 있는 경우 남은 원소 삽입 
		while (lp <= mid) {
			temp[idx] = a[lp];
			idx++;
			lp++;
		}
		
		// 오른쪽 배열에 원소가 남아 있는 경우 남은 원소 삽입 
		while (rp <= right) {
			temp[idx] = a[rp];
			idx++;
			rp++;
		}
		
		// temp의 정렬된 원소 값을 본 배열에 삽입 
		for (int index = left; index <= right; index++) {
			a[index] = temp[index];
		}
	}
}
```

> ⬆️:[Top](#병합-정렬Merge-Sort)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)
> - [합병 정렬 - 위키백과](https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC)
> - [[알고리즘] 합병 정렬(merge sort)이란](https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html)
