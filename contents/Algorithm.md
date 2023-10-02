# 2. Algorithm

#### Contents
- [알고리즘(Algorithm)](#알고리즘Algorithm)
- [시간복잡도(Time Complexity)와 공간복잡도(Space Complexity)](#시간복잡도Time-Complexity와-공간복잡도Space-Complexity)
- [선택 정렬(Selection Sort)](#선택-정렬Selection-Sort)
- [버블 정렬(Bubble Sort)](#버블-정렬Bubble-Sort)
- [삽입 정렬(Insertion Sort)](#삽입-정렬Insertion-Sort)
- [병합 정렬(Merge Sort)](#병합-정렬Merge-Sort)
- [퀵 정렬(Quick Sort)](#퀵-정렬Quick-Sort)
- [힙 정렬(Heap Sort)](#힙-정렬Heap-Sort)
- [계수 정렬(Count Sort)](#계수-정렬Count-Sort)
- [기수 정렬(Radix Sort)](#기수-정렬Radix-Sort)
- [선택 알고리즘(Selection Algorithm)](#선택-알고리즘Selection-Algorithm)
- [이분 탐색(Binary Search)](#이분-탐색Binary-Search)

### 알고리즘(Algorithm)
- 알고리즘
  - 주어진 문제의 해결 절차를 체계적으로 기술한 것
  - 문제 해결 과정을 묘사하는 것
  - 입력으로부터 원하는 출력을 만드는 과정을 기술
  - 문제의 요구조건을 명확히 파악해야 효율적인 알고리즘을 설계할 수 있음
    - 문제의 요구조건은 입력과 출력으로 명시 가능

> ⬆️:[Top](#2-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]

### 시간복잡도(Time Complexity)와 공간복잡도(Space Complexity)
- 시간복잡도와 공간복잡도
  - 제시된 문제의 솔루션이 최적화된 것인지 판단하기 위한 기준
    - 알고리즘의 타당성과 자원 사용 효율성 파악
  - 알고리즘을 수행하는 시스템 및 구성과는 독립적이며, 입력된 수와 상관관계를 나타냄
 
- 점근적 표기법(asymptotic notation)
  - 입력의 크기가 작을 때에는 효율성 문제가 대두되지 않지만 크기가 클 경우에는 알고리즘의 효율성이 중요
  - 입력의 크기가 충분히 큰 경우(n->∞)에 대한 분석을 접근적 분석(asymptotic analysis)이라고 부름
  - O(빅-오, Big-O)
    - 최악의 경우(Worst Case)를 표기
    - 최대로 걸릴 수 있는 시간(상한 시간)을 의미
  - Ω(빅-오메가, Big-Omega)
    - 최선의 경우(Best Case)를 표기
    - 최소로 걸릴 수 있는 시간(하한 시간)을 의미
  - θ(빅-세타, Big-Theta)
    - 최선과 최악이 아닌 경우(Average Case)를 표기
    - 평균적인 복잡도를 의미하지만 복잡한 알고리즘에 사용하기 어려움
  - 최악의 경우에 대한 상한 시간의 성능 파악을 위해 빅-오 표기법이 가장 많이 사용됨
 
- 시간복잡도(Time Complexity)
  - 알고리즘 수행시간에 대한 분석 기준
  - 절대적인 실행 시간과 무관하며 알고리즘을 수행하기 위한 기본 연산이 이루어지는 횟수를 입력 데이터 n에 대한 함수 형태로 표현
    - 기본 연산: 데이터 입출력, 산술 연산, 제어 연산 등
  - 일반적으로 빅-오 표기법으로 표기
  - 연산 횟수가 다항식으로 표현될 경우, 최고차항을 제외한 모든 항과 최고차항의 계수를 제외한다
    - 최고차항의 계수를 제외하는 것은 상수이기에 유의미한 차이가 발생하지 않기 때문
    - Ex) $T(n) = 3n^2 + 10n +100 = O(n^2)$
   
- $O(1)$ 상수 시간(Constant time)
  - 입력의 크기(n)에 상관 없이 항상 일정한 시간이 걸리는 알고리즘
  - 데이터 크기가 성능에 영향을 미치지 않음
  - Stack의 push, pop 연산이 해당

- $O(log n)$ 로그 시간(Logarithmic time)
  - 입력 데이터의 크기가 커질 수록 처리 시간이 로그만큼 짧아지는 알고리즘
  - 이진 트리의 탐색, 재귀의 순기능이 해당

- $O(n)$ 선형 시간(Linear time)
  - 입력 크기(n)에 비례하여 연산 시간이 선형적으로 증가하는 알고리즘
  - 1차원 for문이 해당

- $O(nlog n)$ 선형 로그 시간(Linearithmic time)
  - 입력 크기(n)이 증가할 수록 처리 시간이 로그 배만큼 증가하는 알고리즘
  - 퀵 정렬(quick sort), 병합 정렬(merge sort), 힙 정렬(heap Sort) 등이 해당

- $O(n^2)$ 2차 시간(Quadratic time)
  - 입력 크기(n)이 증가할 수록 처리 시간이 급수적으로 증가하는 알고리즘
  - 이중 for문, 삽입 정렬(insertion sort), 버블 정렬(bubble sort), 선택 정렬(selection sort) 등이 해당

- $O(2^n)$ 지수 시간(Exponential time)
  - 입력 크기(n)이 증가할 수록 처리 시간이 기하급수적으로 증가하는 알고리즘
  - 파보나치 수열, 재귀의 역기능이 해당

<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/Big-O-Complexity-Chart.png" width="600">

- Faster $O(1) < O(log n) < O(n) < O(nlog n) < O(n^2) < O(2^n) < O(n!)$  Slower

- 공간복잡도(Space Complexity)
  - 알고리즘의 메모리 사용량에 대한 분석 기준
  - 최근 메모리 공간이 여유로워져 제약이 많이 줄었으며, 이로 인해 최근 시간복잡도를 공간복잡도보다 우선시 함
  - 최악의 경우(Worst Case)를 산정하며 '빅-오'로 표기
  - 공간복잡도만을 고려할 경우 고정공간보다 가변공간의 자료구조가 효율적
    - 공간 복잡도는 가변공간에 의해 좌우
    - 고정공간(알고리즘과 무관한 공간): 코드 저장 공간, 단순 변수 및 상수
    - 가변공간(알고리즘 실행과 연관된 공간): 실행 중 동적으로 필요한 공간
  - 재귀적, 반복문으로 구현이 가능할 경우 반복문으로 구현하는 것이 공간복잡도 측면에서 좋음
 
> ⬆️:[Top](#2-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [Big-O Algorithm Complexity Cheat Sheet(Know Thy Complexities!)](https://www.bigocheatsheet.com/)
> - [[Algorithm]공간 복잡도(Space Complexity)](https://insight-bgh.tistory.com/506)

### 선택 정렬(Selection Sort)
- 원리

  ![Selection Sort](https://github.com/Minho979/CS_Study/blob/main/contents/images/SelectionSort.gif)

  1\. 첫 번째 원소를 마지막 자료까지 차례대로 비교하여 최소 또는 최대 원소를 선택 

  2\. 최소 값인 경우 첫 번째 자리에 놓고, 최대 값인 경우 마지막 자리에 놓음

  3\. 정렬된 원소를 제외한 나머지 원소에서 해당 과정을 반복

  - 1회전을 수행하고 나면 최소 값이 맨 앞에 있거나 최대 값이 맨 뒤에 위치하게 됨
  
- 시간 복잡도
  - 데이터의 개수 n
  - 데이터 원소의 위치 교환은 상수 시간
  - 루프를 (n-1)번 수행하고, 각 자리에 와야하는 값을 구하기 위해 (n-1), (n-2), ..., 1번의 비교 연산을 수행
    - 비교 연산의 횟수가 전체 수행시간을 좌우
  - (n-1) + (n+2) + ... + 2 + 1 = n(n-1)/2
  - 최선, 평균, 최악의 경우 모두 $O(n^2)$

- 공간 복잡도
  - 주어진 배열 내에서 교환(Swap)으로 정렬하기에 $O(n)$

- 장점
  - 알고리즘이 단순
  - 비교 횟수는 많지만 실제로 교환하는 횟수는 적어 많은 교환이 일어나는 자료에서는 비교적 효율적
  - 정렬하고자 하는 배열 안에서 교환하는 방식으로 다른 별도의 메모리 공간을 필요하지 않음
    - 제자리 정렬(in-place sort): 추가적인 공간을 요구하지 않고 현재 배열 안에서 정렬이 이루어짐

- 단점
  - 시간복잡도가 $O(n^2)$으로 비효율적
  - 불안정 정렬(Unstable Sort)
    - 불안정 정렬: 동일한 값에 대해 기존의 순서가 유지되지 않는 정렬 (Ex. 선택 정렬)
      - Array[1(1), 2, 3(1), 1(2), 3(2)] -> Array[1(2), 1(1), 2, 3(2), 3(1)]
    - 안정 정렬: 동일한 값에 대해 기존의 순서가 유지되는 정렬 (Ex. 버블 정렬, 삽입 정렬)
      - Array[1(1), 2, 3(1), 1(2), 3(2)] -> Array[1(1), 1(2), 2, 3(1), 3(2)]

- 구현 코드
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


> ⬆️:[Top](#2-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)

### 버블 정렬(Bubble Sort)
- 원리

  ![Bubble Sort](https://github.com/Minho979/CS_Study/blob/main/contents/images/BubbleSort.gif)
  
  - 서로 인접한 두 원소를 비교하여 정렬 순서에 맞지 않으면 서로 교환
    - 최대 원소를 가장 뒤로 보내는 효과
  - 같은 방법으로 반복하여 정렬

- 시간 복잡도
  - 데이터 개수 n
  - 데이터 원소의 위치 교환은 상수 시간
  - 최선의 경우 $O(n)$, 평균, 최악의 경우 일정한 비교횟수를 가짐
    - (n-1) + (n+2) + ... + 2 + 1 = n(n-1)/2
  - 최악의 경우와 최선의 경우의 교환 횟수는 변동
    - 역순 정렬인 경우(Worst Case): 한 번의 교환을 위해 3번의 이동 필요
    - 정렬된 경우(Best Case): 자료의 이동이 없음
  - 최선의 경우 $O(n)$
  - 평균, 최의 경우 $O(n^2)$ 

- 공간 복잡도
  - 주어진 배열 내에서 교환(Swap)으로 정렬하기에 $O(n)$

- 장점
  - 제자리 정렬(in-place sort) 알고리즘으로 메모리가 절약된다
  - 안정정렬(Stable Sort)
  - 구현이 간단
- 단점
  - 교환 횟수가 많아 자료의 개수가 많아질 수록 성능 저하 문제가 발생한다
    - 평균, 최악의 경우 $O(n^2)$
   
- 구현 코드 
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


> ⬆️:[Top](#2-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)
> - [[알고리즘] 버블 정렬(bubble sort)이란](https://gmlwjd9405.github.io/2018/05/06/algorithm-bubble-sort.html)

### 삽입 정렬(Insertion Sort)
- 원리

  ![InsertionSort](https://github.com/Minho979/CS_Study/blob/main/contents/images/InsertionSort.gif)

  - 두 번째 원소부터 시작해 그 앞의 원소들과 비교하여 삽입할 위치를 지정
    - 처음 Key 값: 두 번째 원소
  - 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입

- 삽입 정렬 예시
  - 29, 10, 14, 37, 13이 저장된 배열을 오름차순으로 정렬

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/InsertionSortEx.png" width="630">
 
- 시간 복잡도
  - 최악의 경우(역순 정렬인 경우)에는 선택, 버블 정렬과 마찬가지로 $O(n^2)$
  - 최선의 경우(정렬되어 있는 경우)에는 비교연산을 한번씩 수행하기에 $O(n)$
    - 이미 정렬된 배열에 자료를 삽입/삭제하는 경우 최적의 알고리즘에 해당
    - 이는 탐색을 제외한 오버헤드가 매우 적기 때문
  - 최선의 경우: $O(n)$, 평균 & 최악의 경우: $O(n^2)$

- 공간 복잡도
  - 주어진 배열 내에서 교환(Swap)으로 정렬하기에 $O(n)$

- 장점
  - 알고리즘이 단순
  - 정렬된 배열인 경우 매우 효율적
  - 제자리 정렬(in-place sort) 알고리즘으로 메모리가 절약
  - 안정정렬(Stable Sort)

- 단점
  - 비교적 많은 원소들이 이동
  - 평균, 최악의 경우 시간 복잡도가 $O(n^2)$로 비효율적
  - 자료의 수가 많고 크기가 클 경우 부적

- 구현 코드
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

> ⬆️:[Top](#2-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)

### 병합 정렬(Merge Sort)
- 개념

  ![MergeSort](https://github.com/Minho979/CS_Study/blob/main/contents/images/MergeSort.gif)

  - 하나의 리스트를 균등한 크기로 분할하고, 분할된 부분 리스트들을 독립적으로 정렬한 후 정렬된 부분 리스트를 합하여 전체 리스트 정렬함
    - 분할 정복(Divide and Conquer) 알고리즘 기반
  - 데이터를 비교하면서 찾기 때문에 비교 정렬
  - 추가적인 공간이 필요하기에 제자리 정렬(in-place sort)이 아님
  - 최대한 잘게 쪼개어 앞부분의 리스트부터 합치기 때문에 안정정렬(Stable Sort) 알고리즘
  - n개의 부분 리스트로 분할하는 방법(n-way)과 2개의 부분 리스트로 분할하는 (2-way)방법이 존재
    - 하향식 2-way 합병 정렬을 자주 사용 

- 병합 정렬의 과정
  - 분할(Divide): 입력 배열을 같은 크기의 2개의 부분 배열로 분할
  - 정복(Conquer): 부분 배열을 정렬, 부분 배열의 크기가 충분히 작지 않으면 재귀 호출을 이용해 다시 분할 정복 방법을 적용
    - 분할된 부분 배열의 크기가 1이 아닌 경우 분할과정부터 다시 수행
  - 결합(Combine): 정렬된 부분 배열들을 하나의 배열에 병합
  1. 2개의 리스트 값들을 처음부터 하나씩 비교하여 더 작은 값을 보조 리스트에 이동
  2. 둘 중 하나가 끝날 때까지 반복
  3. 두 개의 리스트 중 하나의 리스트가 먼저 끝날 경우 나머지 리스트의 값을 전부 보조 리스트에 복사
  4. 4. 보조 리스트의 값을 기존의 리스트로 복사

 - 예시
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/MergeSort.png" width="630">
  
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/MergeSortCombine.png" width="630">
 	
   - 부분 리스트의 처음 값 부터 비교하여 정렬하기에 안정 정렬(Stable Sort)가 보장

- 시간 복잡도

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

- 공간 복잡도
  - 보조 리스트를 이용하여 정렬하므로 $O(n)$
 
- 특징
  - 추가적인 리스트(공간)이 필요
  - 각 부분 배열을 정렬할 때도 병합 정렬을 재귀적으로 호출하여 적용
  - 2개의 리스트를 병합(merge)하는 단계에서만 실제로 정렬이 이루어짐

- 장점
  - 안정 정렬(Stable Sort)
  - 항상 부분 리스트로 쪼개어 작동하기에 데이터의 크기와 관계없이 항상 $O(nlogn)$ 보장하기에 안정적
  - 레코드를 연결 리스트로 구현할 시 데이터의 이동 시간이 매우 작아져 큰 레코드 정렬 시 효율적
    - 연결 리스트로 구현할 시 링크 인덱스 값만 변경되며 제자리 정렬(in-place sort)로 구현 가능
- 단점
  - 제자리 정렬(in-place sort)가 아니기에 추가 메모리 공간 O(n)이 필요
  - 정렬된 원소들을 본 리스트로 복사하는 과정이 많은 시간이 소요
    - 레코드들의 크기가 큰 경우 이동 횟수가 많아지기에 시간 낭비가 증가

- 구현 코드
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

> ⬆️:[Top](#2-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)
> - [합병 정렬 - 위키백과](https://ko.wikipedia.org/wiki/%ED%95%A9%EB%B3%91_%EC%A0%95%EB%A0%AC)
> - [[알고리즘] 합병 정렬(merge sort)이란](https://gmlwjd9405.github.io/2018/05/08/algorithm-merge-sort.html)

### 퀵 정렬(Quick Sort)
- 개념

  ![Quick Sort](https://github.com/Minho979/CS_Study/blob/main/contents/images/QuickSort.gif)

  - 하나의 리스트를 피벗(pivot)을 중심으로 두 개의 비균등한 크기로 분할하고 분할된 부분 리스트를 정렬한 후 두 리스트를 병합하여 정렬
    - 피벗(pivot): 리스트 안에 있는 원소 중 선택한 하나의 원소, 중앙 값에 가까운 값일 수록 성능 향
    - 분할 정복(Divide and Conquer) 알고리즘: 문제를 분할하여 각각 해결한 다음 병합을 통해 원래의 문제 해결, 재귀호출을 이용하여 구현
  - 한쪽으로 치우치지만 않으면 평균적으로 매우 빠른 수행 속도를 보임
  - 불안정 정렬(Unstable sort)
  - 다른 원소와 비교만을 통해 정렬을 수행하는 '비교 정렬'

- 퀵 정렬의 과정
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

- 시간 복잡도
  - 최선의 경우(균등하게 나뉘어지는 경우) 
    
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/QuickSortTimeComplexity-Best.png" width="630">
    
    - 비교 횟수: 재귀 호출의 깊이(단계 수) * 각 순환 호출 단계의 비교 연산
      - 깊이: 레코드 개수 n이 2의 거듭 제곱$(n=2^k)$일 경우  $k=logn$
      - 비교: 전체 리스트의 대부분의 레코드를 비교하므로 평균 $n$
      - $nlogn$
    - 이동 횟수: 비교 횟수보다 적으므로 무시할 수 있음
    - $O(nlogn)$

  - 최악의 경우(불균형하게 나누어지는 경우, 이미 정렬된 리스트에 대해 퀼 정렬을 하는 경우)
    
    <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/QuickSortTimeComplexity-Worst.png" width="500">

    - 비교 횟수: 재귀 호출의 깊이(단계 수) * 각 순환 호출 단계의 비교 연산
      - 깊이: $n$, 비교: $n$
      - $n^2$
    - 이동 횟수: 비교 횟수보다 적으므로 무시할 수 있음
    - $O(n^2)$

  - 평균적인 경우 $O(nlogn)$

- 공간 복잡도
  - 배열 안에서 교환하기에 $O(n)$
  - 재귀호출 공간 $O(logn)$
 
- 특징
  - 상대적으로 작은 메모리만을 사용하기에 제자리 정렬(in-place) 정렬이라고 기술하기도 함
    - 공간 복잡도 $O(n), O(logn)$
  - 최악의 경우를 제외하고 매우 빠른 수행 속도를 보임
    - 최악의 경우: 피벗이 한쪽으로 치우친 경우
  - 중복된 키 값의 위치가 정렬 과정에서 바뀔 수 있으므로 불안정 정렬(Unstable sort)
  - 시간 복잡도가 $O(nlogn)$으로 동일한 다른 정렬 알고리즘과 비교했을 때 가장 빠름
    - 불필요한 데이터의 이동을 줄이고 먼 거리의 데이터를 교환하며, 한번 결정된 피벗들이 이후 연산에서 제외되는 특성때문

- 장점
  - 속도가 빠르다
    - 시간 복잡도가 O(nlogn)를 가지는 다른 정렬 알고리즘과 비교했을 때도 가장 빠른 속도
  - 추가적인 메모리 공간을 필요로 하지 않음
    - 재귀 호출의 깊이에 따라 $O(logn)$의 메모리를 필요로 함

- 단점
  - 정렬된 리스트에 대해 퀼 정렬의 불균형 분할에 의해 수행시간이 $O(n^2)$으로 버블 정렬과 다를 것 없는 성능을 보임
    - 이를 방지하기위해 피벗을 선택할 때 균등하게 분할할 수 있는 데이터를 선택

- 구현 코드
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

> ⬆️:[Top](#2-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)
> - [[알고리즘] 퀵 정렬(quick sort)이란](https://gmlwjd9405.github.io/2018/05/10/algorithm-quick-sort.html)
> - [자바 [JAVA] - 퀵 정렬 (Quick Sort)](https://st-lab.tistory.com/250)

### 힙 정렬(Heap Sort)
- [힙이란?](https://github.com/Minho979/CS_Study/blob/main/contents/Data%20Structure/Binary%20Heap.md)

- 개념
  
  ![HeapSort](https://github.com/Minho979/CS_Study/blob/main/contents/images/HeapSort.gif)

  - 최대 힙 트리나 최소 힙 트리를 구성해 정렬을 하는 방법
    - 내림차순 정렬은 최대 힙을 이용하고, 오름차순 정렬은 최소 힙을 이용
  - 불안정 정렬(Unstable Sort)
  - 제자리 정렬(in-place sort)

- 힙 정렬의 과정
  - 내림차순 
    1. 정렬해야 할 n개의 요소들로 최대 힙(완전 이진 트리)을 구성
    2. 한 번에 하나씩 요소를 힙에서 꺼내서 배열의 뒤에서부터 저장하고 힙의 사이즈를 1 감소
       - 루트 노드 값을 반환하고 기존 루트 값을 마지막 요소 값과 바꾼 후 힙 사이즈를 감소 (실제로 삭제되는 것은 마지막 노드)
    3. 삭제되는 요소(최대값)들은 값이 감소되는 순서로 배열 뒤에서부터 정렬되게 됨
    4. 힙의 사이즈가 1보다 크면 위의 과정을 반복

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/MaxHeap.gif" width="350">
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/MaxHeap-Del.gif" width="350">
  
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/Heap_del.png" width="600">

- 시간 복잡도
  - 트리의 높이가 완전 이진 트리의 높이인 $logn$이므로 힙에 원소 삽입, 삭제로 재정비하는 시간 $logn$
  - 요소의 개수는 n개 이므로 전체적으로 $O(nlogn)$시간이 소요
  - 최선, 평균, 최악 모두 $O(nlogn)$의 시간복잡도를 가짐
  
- 공간 복잡도
  - 추가적인 메모리를 필요로 하지 않는 제자리 정렬로 $O(n)$

- 장점
  - 어떠한 입력 데이터에 대해서도 $O(nlogn)$ 시간 복잡도를 보장
  - 추가적인 메모리 용량이 필요 없음
 
- 단점
  - 실제 프로그램에서 실행되는 경우 평균적인 연산 속도가 퀵 정렬보다 느리고, 불안정함

- 힙 정렬이 유용한 상황
  - 최대 값 또는 최소 값을 몇 개를 구할 때
    - 최소 힙 or 최대 힙의 루트 값이기 때문에 한번의 힙 구성을 통해 값을 구할 수 있음
  - 최대 k만큼 떨어진 요소들을 정렬할 때
    - 삽입 정렬보다 개선된 결과를 얻을 수 있음

- 구현 코드
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

> ⬆️:[Top](#2-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)
> - [[알고리즘] 힙 정렬(heap sort)이란](https://gmlwjd9405.github.io/2018/05/10/algorithm-heap-sort.html)
> - [Heap Data Structures](https://www.tutorialspoint.com/data_structures_algorithms/heap_data_structure.htm)

### 계수 정렬(Count Sort)
- 개념
  - 비교 연산을 사용하지 않고, 배열 내에서 특정 값이 등장하는 횟수를 통해 정렬을 수행

- 제약 사항
  - 데이터 값은 양수
  - 데이터 값의 범위가 O(n) 범위에 있을 때 사용 가능
    - 값의 범위가 메모리 사이즈가 넘지 않도록 너무 크지 않아야 함

- 계수 정렬 과정

  1\. 입력 받은 배열 A의 요소 값의 등장 횟수를 카운팅할 배열 Count와 최종적으로 정렬된 값을 담을 배열 B를 설정

  2\. 배열 A에서 값을 하나씩 꺼내 해당 값을 Count의 인덱스로 사용해 Count의 요소 값을 하나 증가
     - Count[A[i]]++
  
  3\. Count가 완성되면 Count의 각 요소들을 누적합으로 합산
     - Count[i] = Count[i] + Count[i-1]
  
  4\. A의 가장 뒤에서부터 값을 꺼내 해당 값을 Count의 인덱스로 사용하고 참조된 B의 값을 하나 감소
     - Count[A[i]]--
  
  5\. 감소된 B의 값을 C의 인덱스로 사용해 A에서 꺼낸 값을 삽입
     - B[Count[A[i]]] = A[i]
  
  6\. A의 모든 요소에 대해 4번 5번 과정을 반복한다 

- 예시

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/CountSortEx1.png" width="500">
  
  - 배열 A를 입력받고 배열 Count와 B를 준비
    - 이때 Count의 크기는 A의 Value 값이 B의 인덱스이므로 A의 `최대값 +1`으로 설정
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/CountSortEx2.png" width="500">

  - A를 순회하며 등장하는 값들의 등장 횟수를 Count에 저장 `Count[A[i]]++`
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/CountSortEx3.png" width="500">

  - 1차로 완성된 Count를 누적 합으로 업데이트 `Count[i] = Count[i] + Count[i-1]`
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/CountSortEx4.png" width="500">

  - A의 맨 뒤에서부터 값을 하나씩 꺼내서 Count 인덱스로 접근 후 하나 감소 `Count[A[i]]--`
    - 배열 Count에서 3번 인덱스의 값은 6으로 이는 배열 A에 3보다 작거나 같은 수가 6개 존재한다는 의미
  - 해당 값을 B의 인덱스로 접근 후 꺼낸 값을 저장 `B[Count[A[i]]] = A[i]`
  - A[0]까지 반복
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/CountSortEx5.png" width="500">

  - 반복하여 정렬 완료


- 시간 복잡도
  - Count 배열 생성에 필요한 시간 $O(n)$
  - Count 배열 뒤에서부터 순회하여 값을 채우는 시간 $O(n)$
  - 최악의 경우 $O(n+k)$
    - k는 음이 아닌 키 값의 범위를 의미
  - $O(n)$
    - Why? n에 비하면 k의 값은 상수로 보아도 무관

- 공간 복잡도
  - 추가적인 배열을 생성하기에 $O(n)$

- 장점
  - 비교 연산이 없어 빠른 수행시간 $O(n)$을 보장
    - 해당 성능을 보장하기 위해서는 데이터의 명확한 제한이 필요
  - 안정 정렬(Stable Sort)

- 단점
  - 정렬을 하기 위한 추가적인 메모리가 필요
  - 카운팅을 하기 위한 배열의 길이가 최대값에 의해 결정되어 메모리 낭비가 발생할 수 있음
  - 데이터의 수보다 배열의 크기가 클 경우 비효율적
    - (1, 10000) 두 개의 값만 가지더라도 Count 배열의 크기는 10001
  - 음수가 섞인 경우 사용 불가하며 명확한 데이터 제한이 필요
 
- 구현 코드
``` java
public class CountSort {

	public static void countSort(int[] a) {
		// count 배열 생성 (수의 범위 1~3)
		int[] count = new int[4];
		
		/* 
		교체 작업을 진행할 a의 값을 가진 배열 (예제 A배열에 해당)
		void 이므로 B에 해당하는 배열은 매개변수 a
		*/
		int[] sorted = new int[a.length]; 
		
		for (int i = 0; i < a.length; i++) {
			sorted[i] = a[i];
		}
		
		// 원소 개수 count
		for (int i = 0; i < a.length; i++) {
			count[a[i]] ++;
		}
		
		// 누적 합 
		for (int i = 1; i < count.length; i++) {
			count[i] += count[i-1];
		}
		
		// 교체 작업 
		for (int i = a.length -1; i >= 0; i--) {
			int value = sorted[i];
			count[value]--; // 최대 개수가 인덱스 범위 밖이기에 선차감 
			a[count[value]] = value;
		}		
	}
	
	public static void main(String[] args) {
		int[] a = {1, 2, 1, 1, 3, 3};
		countSort(a);
		for (int i =0; i<a.length; i++){
			System.out.printf(" %d", a[i]);
		}

	}

}

```

> ⬆️:[Top](#2-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [알고리즘 6일차 - O(n) 정렬, 계수 정렬](https://velog.io/@chappi/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-6%EC%9D%BC%EC%B0%A8-On-%EC%A0%95%EB%A0%AC-%EA%B3%84%EC%88%98-%EC%A0%95%EB%A0%AC)


### 기수 정렬(Radix Sort)
- 개념
  - 비교 연산을 수행하지 않아 조건이 충족하는 상황이라면 매우 빠른 속도를 보장
  - 데이터의 각 자리수를 낮은 자리수부터 가장 큰 자리수까지 차례대로 올라가며 정렬
  - 기수에 따른 추가 버킷 공간이 필요
    - Ex) 10진수 -> 기수 10 -> 버킷 10개 요구
    - 버킷: 기수만큼 Queue를 이용해 만든 저장공간
    - [Queue란?](https://github.com/Minho979/CS_Study/blob/main/contents/Data%20Structure/Queue.md)
  - 안정정렬
 
- 기수 정렬 과정

  1\. 현재 데이터들 중 가장 큰 자리수를 파악
  
  2\. 각 데이터들의 1의 자리를 비교하여 오름차순 정렬
  
  3\. 그 뒤 10의 자리수를 비교하여 오름차순 정렬
  
  4\. 3번의 과정에서 10의 자리가 없다면 0으로 간주
  
  5\. 위의 과정을 가장 큰 자리수까지 반복

- 예시
  
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RadixSort1.png" width="500">
  
  - 최대 자리수 두자리 10진수 -> 버킷 10개, 정렬 2단계 수행
  
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RadixSort2.png" width="500">

  - 각 원소를 일의 자리 값에 따라서 순서대로 버킷 분배
  
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RadixSort3.png" width="500">

  - 버킷에 분배된 원소들을 순서대로 꺼내서 저장
  
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RadixSort4.png" width="500">

  - 각 원소를 십의 자리 값에 따라서 순서대로 버킷 분배
  
  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RadixSort5.png" width="500">

  - 버킷에 분배된 원소들을 순서대로 꺼내서 저장하여 정렬 종료
  - 더 긴 자리의 경우 백의 자리, 천의 자리 등에 대해 동일한 과정을 반복하여 정렬할 수 있음 

- 시간 복잡도
  - 정렬할 원소의 수(n), 가장 긴 값의 자리수(d), 버킷 수를 결정하는 기수(r)의 영향을 받음
  - 정렬할 원소 n개를 r개의 버킷에 분배하고 다시 꺼내 합치는 작업: $O(n+r)$ 
  - 위의 작업을 자리수 d만큼 반복하므로 $O(d(n+r))$
  - d와 r의 경우 n에 비하면 상수라 봐도 무관함
  - 모든 경우에서 $O(n)$

- 공간 복잡도
  - 기수만큼의 버킷 공간을 요구하기에 $O(n+r)$
  - r은 기수의 크기이기에 n에 비해 무시할 수 있는 상수로 볼 수 있음
  - $O(n)$

- 장점
  - 자리수의 값을 비교하여 정렬하는 방식이기에 문자열, 정수 등을 빠른 속도로 정렬 가능
  - 동일 값이 있어도 변하지 않는 안정정렬(Stable Sort)
  - 시간 복잡도는 $O(n)$으로 매우 빠른 수행 속도를 보장

- 단점
  - 적용할 수 있는 범위가 제한적
    - 아스키로 표현 가능한 정수, 알파벳, 특수문자 등은 가능하지만 소수는 불가능함
  - 기수만큼의 추가 메모리 공간(버킷 공간)을 요구함
    - 비 제자리 정렬(out of place sort) 
  - 버킷의 크기를 모든 케이스에 알맞게 정의하기 어려움
 
- 구현 코드
```java
import java.util.LinkedList;
import java.util.Queue;

public class RadixSort {
	
	public static void radixSort(int[] a, int bucketSize) {
		
		// bucket 생성 및 초기화 
		Queue<Integer>[] bucket = new LinkedList[bucketSize];
		for (int i = 0; i < bucketSize; i++) {
			bucket[i] = new LinkedList<>(); 
		}
		
		int maxLen = maxDigitCount(a); // 최대 자리수 저장 변수 
		
		int divfac = 1;		       // 나눠주는 요소 
		
		int size = a.length;	       // 배열 길이 
		
		/*
		 배열 원소들을 버킷에 삽인 후 삭제하여 
		 재배열하는 과정을 자리수의 크기(maxLen)번 반복 
		 */
		for (int d = 0; d < maxLen; d++) {
			/*
			 값을 divfac으로 나누고 %10을 통해 
			 나머지를 구한 뒤 radix 저장하고 
			 radix를 인덱스로 하는 bucket에 a[i] 값 저장 
			 */
			for (int i = 0; i < size; i++) {
				int radix = (a[i] / divfac) % 10;
				bucket[radix].add(a[i]);
			}
			
			int ap = 0; // array index pointer
			
			for (int i = 0; i < bucketSize; i++) {
				/*
				 bucket[i]가 빈 상태가 아닐 때 
				 bucket[i]에서 값을 꺼내어 
				 a[ap]에 저장 후 ap++ 
				 */
				while (!bucket[i].isEmpty()) {
					a[ap++] = bucket[i].remove();
				}
			}
			
			divfac *= 10; // 나눠주는 요소에 10 곱해 자리수 이동
		}
	}
	
	
	// 원소 중 가장 큰 자리수를 반환 
	private static int maxDigitCount(int[] a) {
		int max = 0;
		
		// 최대값을 구함
		for (int i = 0; i < a.length; i++) {
			if (max < a[i]) {
				max = a[i];
			}
		}
		
		/*
		 숫자의 자리수를 구하는 연산
		 log10을 취해주면 자리수가 나옴 
		 log10(10) = 1, log10(100) = 2
		 maxDigitCount(10) = 2 
		 maxDigitCount(2301) = 4
		 */
		max = (int) Math.log10(max)+1;
		
		return max;

	}

	public static void main(String[] args) {
		final int bucketSize = 10;
		
		int[] a = {30, 20, 4, 2, 33, 6, 2000, 300, 312, 31, 55, 3, 22, 6, 34, 2301, 32};
		radixSort(a, bucketSize);
		for (int i =0; i<a.length; i++){
			System.out.printf(" %d", a[i]);
		}

	}

}

```

> ⬆️:[Top](#2-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [[JAVA] 기수 정렬 (Radix Sort)](https://banjjak1.tistory.com/52)

### 선택 알고리즘(Selection Algorithm)
- 개념
  

> ⬆️:[Top](#2-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]

### 이분 탐색(Binary Search)
- 개념

> ⬆️:[Top](#2-Algorithm)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#2-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
