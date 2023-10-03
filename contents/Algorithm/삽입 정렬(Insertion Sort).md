# 삽입 정렬(Insertion Sort)
## 원리

  ![InsertionSort](https://github.com/Minho979/CS_Study/blob/main/contents/images/InsertionSort.gif)

  - 두 번째 원소부터 시작해 그 앞의 원소들과 비교하여 삽입할 위치를 지정
    - 처음 Key 값: 두 번째 원소
  - 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입

## 삽입 정렬 예시
  - 29, 10, 14, 37, 13이 저장된 배열을 오름차순으로 정렬

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/InsertionSortEx.png" width="630">
 
## 시간 복잡도
  - 최악의 경우(역순 정렬인 경우)에는 선택, 버블 정렬과 마찬가지로 $O(n^2)$
  - 최선의 경우(정렬되어 있는 경우)에는 비교연산을 한번씩 수행하기에 $O(n)$
    - 이미 정렬된 배열에 자료를 삽입/삭제하는 경우 최적의 알고리즘에 해당
    - 이는 탐색을 제외한 오버헤드가 매우 적기 때문
  - 최선의 경우: $O(n)$, 평균 & 최악의 경우: $O(n^2)$

## 공간 복잡도
  - 주어진 배열 내에서 교환(Swap)으로 정렬하기에 $O(n)$

## 장점
  - 알고리즘이 단순
  - 정렬된 배열인 경우 매우 효율적
  - 제자리 정렬(in-place sort) 알고리즘으로 메모리가 절약
  - 안정정렬(Stable Sort)

## 단점
  - 비교적 많은 원소들이 이동
  - 평균, 최악의 경우 시간 복잡도가 $O(n^2)$로 비효율적
  - 자료의 수가 많고 크기가 클 경우 부적

## 구현 코드
``` java
public class InsertionSort {
	
	public static void insertionSort(int [] a) {
		int i, j, loc, size;
		size = a.length;
		
		for (i = 1; i < size; i++) {
			
			loc = a[i]; // 지정 Key 값
			
			j = i - 1;

			// 지정 값이 이전 원소보다 크기 전까지 반복, loc <  a[j]는 안정정렬을 위해 키 값이 같을 때 이동 방지
			while(j >= 0 && loc < a[j]) {
				a[j+1] = a[j];	// 원소를 한 칸 씩 뒤로 이동
				j--;
			}

			/*
			해당 루프를 탈출하는 경우 loc의 원소가 앞의 원소보다 크다는 의미
			loc 원소를 j의 뒤로 보내야함
			*/
			a[j + 1] = loc;
			
		}
	}
}
```

> ⬆️:[Top](#삽입-정렬Insertion-Sort)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)
