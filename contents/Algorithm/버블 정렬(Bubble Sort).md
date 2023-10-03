# 버블 정렬(Bubble Sort)
## 원리

  ![Bubble Sort](https://github.com/Minho979/CS_Study/blob/main/contents/images/BubbleSort.gif)
  
  - 서로 인접한 두 원소를 비교하여 정렬 순서에 맞지 않으면 서로 교환
    - 최대 원소를 가장 뒤로 보내는 효과
  - 같은 방법으로 반복하여 정렬

## 시간 복잡도
  - 데이터 개수 n
  - 데이터 원소의 위치 교환은 상수 시간
  - 최선의 경우 $O(n)$, 평균, 최악의 경우 일정한 비교횟수를 가짐
    - (n-1) + (n+2) + ... + 2 + 1 = n(n-1)/2
  - 최악의 경우와 최선의 경우의 교환 횟수는 변동
    - 역순 정렬인 경우(Worst Case): 한 번의 교환을 위해 3번의 이동 필요
    - 정렬된 경우(Best Case): 자료의 이동이 없음
  - 최선의 경우 $O(n)$
  - 평균, 최의 경우 $O(n^2)$ 

## 공간 복잡도
  - 주어진 배열 내에서 교환(Swap)으로 정렬하기에 $O(n)$

## 장점
  - 제자리 정렬(in-place sort) 알고리즘으로 메모리가 절약된다
  - 안정정렬(Stable Sort)
  - 구현이 간단
## 단점
  - 교환 횟수가 많아 자료의 개수가 많아질 수록 성능 저하 문제가 발생한다
    - 평균, 최악의 경우 $O(n^2)$
   
## 구현 코드 
``` java
public class BubbleSort {
	
	public static int[] bubbleSort(int a[]) {
		int i, j, size;
		size = a.length;

		// 배열의 길이 만큼 반복
		for (i = 0; i < size; i++) {
			boolean sorted = true;
			// 마지막 원소는 정렬된 상태 이므로 끝을 제외한 나머지 길이 만큼 반복, 큰 원소 교환
			for(j = 0; j < size - 1 -i; j++) {
				if (a[j] > a[j+1]) {
					swap(a, j, j+1);
					sorted = false;
				}
			}
			if (sorted == true) break;
		}
		return a;
	}
	
	public static void swap(int a[], int i, int j) {
		int temp = a[i];
		a[i] = a[j];
		a[j] = temp;
	}
}
```


> ⬆️:[Top](#버블-정렬Bubble-Sort)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)
> - [[알고리즘] 버블 정렬(bubble sort)이란](https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html)
