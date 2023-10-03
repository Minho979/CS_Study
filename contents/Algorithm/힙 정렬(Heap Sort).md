# 힙 정렬(Heap Sort)
## 개념
  
  ![HeapSort](https://github.com/Minho979/CS_Study/blob/main/contents/images/HeapSort.gif)

  - 최대 힙 트리나 최소 힙 트리를 구성해 정렬을 하는 방법
    - 내림차순 정렬은 최대 힙을 이용하고, 오름차순 정렬은 최소 힙을 이용
    - [힙(Heap)이란?](https://github.com/Minho979/CS_Study/blob/main/contents/Data%20Structure/Binary%20Heap.md)
  - 불안정 정렬(Unstable Sort)
  - 제자리 정렬(in-place sort)

## 힙 정렬의 과정
  - 내림차순 
    1. 정렬해야 할 n개의 요소들로 최대 힙(완전 이진 트리)을 구성
    2. 한 번에 하나씩 요소를 힙에서 꺼내서 배열의 뒤에서부터 저장하고 힙의 사이즈를 1 감소
       - 루트 노드 값을 반환하고 기존 루트 값을 마지막 요소 값과 바꾼 후 힙 사이즈를 감소 (실제로 삭제되는 것은 마지막 노드)
    3. 삭제되는 요소(최대값)들은 값이 감소되는 순서로 배열 뒤에서부터 정렬되게 됨
    4. 힙의 사이즈가 1보다 크면 위의 과정을 반복

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/MaxHeap.gif" width="350">
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/MaxHeap-Del.gif" width="350">
  
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/Heap_del.png" width="600">

## 시간 복잡도
  - 트리의 높이가 완전 이진 트리의 높이인 $logn$이므로 힙에 원소 삽입, 삭제로 재정비하는 시간 $logn$
  - 요소의 개수는 n개 이므로 전체적으로 $O(nlogn)$시간이 소요
  - 최선, 평균, 최악 모두 $O(nlogn)$의 시간복잡도를 가짐
  
## 공간 복잡도
  - 추가적인 메모리를 필요로 하지 않는 제자리 정렬로 $O(n)$

## 장점
  - 어떠한 입력 데이터에 대해서도 $O(nlogn)$ 시간 복잡도를 보장
  - 추가적인 메모리 용량이 필요 없음
 
## 단점
  - 실제 프로그램에서 실행되는 경우 평균적인 연산 속도가 퀵 정렬보다 느리고, 불안정함

- 힙 정렬이 유용한 상황
  - 최대 값 또는 최소 값을 몇 개를 구할 때
    - 최소 힙 or 최대 힙의 루트 값이기 때문에 한번의 힙 구성을 통해 값을 구할 수 있음
  - 최대 k만큼 떨어진 요소들을 정렬할 때
    - 삽입 정렬보다 개선된 결과를 얻을 수 있음

## 구현 코드
``` java
public class HeapSort {
	
	public static void heapSort(int a[], int size) {
		heapify(a, size);  // 힙 구조로 재구성
		
		// 루트 원소 제거 후 마지막 원소를 루트로 이동 
		for (int i = size -1; i >= 0; i--) {
			swap(a, 0, i); // 루트와 마지막 원소 교환 
			heapify(a, i); // 남은 요소들을 대상으로 최대힙 재구성 
		}
	}
	
	// 최대 힙 구성 
	public static void heapify(int a[], int last) {
		// last = last index
		
		// i가 1부터 시작하는 이유는 0은 루트
		for(int i = 1; i < last; i++) {
			int child = i; // 자식 인덱스 
			
			while (child > 0) {
				int parent = (child -1) / 2; // 부모 인덱스 계산
				
				// 자식이 부모보다 큰 경우 서로 swap
				if (a[child] > a[parent]) {
					swap(a, child, parent);
				}
				/*
				 자식 인덱스를 부모 인덱스 값으로 조정하여 
				 child index가 0이 될 때까지 
				 자식이 부모보다 큰 경우를 찾아 스왑
				 0이 되는 경우 루트 노드와의 비교까지 마친 상황이므로 
				 더 이상 반복할 필요가 없음 
				 */
				child = parent; 
			}
		}
	}
	
	public static void swap(int a[], int i, int j) {
		int temp = a[i];
		a[i] = a[j];
		a[j]= temp;
		
	}
}
```

> ⬆️:[Top](#힙-정렬Heap-Sort)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)
> - [[알고리즘] 힙 정렬(heap sort)이란](https://gmlwjd9405.github.io/2018/05/10/algorithm-heap-sort.html)
> - [Heap Data Structures](https://www.tutorialspoint.com/data_structures_algorithms/heap_data_structure.htm)
