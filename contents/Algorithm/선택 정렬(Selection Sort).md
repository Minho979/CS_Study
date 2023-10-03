# 선택 정렬(Selection Sort)
## 원리

  ![Selection Sort](https://github.com/Minho979/CS_Study/blob/main/contents/images/SelectionSort.gif)

  1\. 첫 번째 원소를 마지막 자료까지 차례대로 비교하여 최소 또는 최대 원소를 선택 

  2\. 최소 값인 경우 첫 번째 자리에 놓고, 최대 값인 경우 마지막 자리에 놓음

  3\. 정렬된 원소를 제외한 나머지 원소에서 해당 과정을 반복

  - 1회전을 수행하고 나면 최소 값이 맨 앞에 있거나 최대 값이 맨 뒤에 위치하게 됨
  
## 시간 복잡도
  - 데이터의 개수 n
  - 데이터 원소의 위치 교환은 상수 시간
  - 루프를 (n-1)번 수행하고, 각 자리에 와야하는 값을 구하기 위해 (n-1), (n-2), ..., 1번의 비교 연산을 수행
    - 비교 연산의 횟수가 전체 수행시간을 좌우
  - (n-1) + (n+2) + ... + 2 + 1 = n(n-1)/2
  - 최선, 평균, 최악의 경우 모두 $O(n^2)$

## 공간 복잡도
  - 주어진 배열 내에서 교환(Swap)으로 정렬하기에 $O(n)$

## 장점
  - 알고리즘이 단순
  - 비교 횟수는 많지만 실제로 교환하는 횟수는 적어 많은 교환이 일어나는 자료에서는 비교적 효율적
  - 정렬하고자 하는 배열 안에서 교환하는 방식으로 다른 별도의 메모리 공간을 필요하지 않음
    - 제자리 정렬(in-place sort): 추가적인 공간을 요구하지 않고 현재 배열 안에서 정렬이 이루어짐

## 단점
  - 시간복잡도가 $O(n^2)$으로 비효율적
  - 불안정 정렬(Unstable Sort)
    - 불안정 정렬: 동일한 값에 대해 기존의 순서가 유지되지 않는 정렬 (Ex. 선택 정렬)
      - Array[1(1), 2, 3(1), 1(2), 3(2)] -> Array[1(2), 1(1), 2, 3(2), 3(1)]
    - 안정 정렬: 동일한 값에 대해 기존의 순서가 유지되는 정렬 (Ex. 버블 정렬, 삽입 정렬)
      - Array[1(1), 2, 3(1), 1(2), 3(2)] -> Array[1(1), 1(2), 2, 3(1), 3(2)]

## 구현 코드
``` java
public class SelectionSort {
	
	public static void selectionsort(int a[]) {
		int i, j, min, size;
		
		size = a.length;
		
		for(i = 0; i < size - 1; i++) {
			min = i;
			
			// 최솟값 인덱스 찾기 
			for(j=i+1; j<size; j++) {
				if(a[j] < a[min]) {
					min = j;
				}
			}
			
			// i번쨰 값과 최솟값의 위치를 서로 교환 
			swap(a, min, i);		
		}
	}
	
	public static void swap(int a[], int i, int j) {
		int temp = a[i];
		a[i] = a[j];
		a[j] = temp;
	}
}
```


> ⬆️:[Top](#선택-정렬Selection-Sort)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)
