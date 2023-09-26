# 2. Algorithm

#### Contents
- [알고리즘(Algorithm)](#알고리즘Algorithm)
- [시간복잡도(Time Complexity)와 공간복잡도(Space Complexity)](#시간복잡도Time-Complexity와-공간복잡도Space-Complexity)
- [선택 정렬(Selection Sort)](#선택-정렬Selection-Sort)
- [버블 정렬(Bubble Sort)](#버블-정렬Bubble-Sort)
- [삽입 정렬(Insertion Sort)](#삽입-정렬Insertion-Sort)

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

![Big-O Complexity Chart](https://github.com/Minho979/CS_Study/blob/main/contents/images/Big-O-Complexity-Chart.png)

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
  
  1\. 첫 번째 원소를 마지막 자료까지 차례대로 비교하여 최소 또는 최대 원소를 선택 

  2\. 최소 값인 경우 첫 번째 자리에 놓고, 최대 값인 경우 마지막 자리에 놓음

  3\. 정렬된 원소를 제외한 나머지 원소에서 해당 과정을 반복

  - 1회전을 수행하고 나면 최소 값이 맨 앞에 있거나 최대 값이 맨 뒤에 위치하게 됨
  
  ![Selection Sort](https://github.com/Minho979/CS_Study/blob/main/contents/images/SelectionSort.gif)

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
    - 제자리 정렬(in-place sorting): 추가적인 공간을 요구하지 않고 현재 배열 안에서 정렬이 이루어짐

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
  - 서로 인접한 두 원소를 비교하여 정렬 순서에 맞지 않으면 서로 교환
    - 최대 원소를 가장 뒤로 보내는 효과
  - 같은 방법으로 반복하여 정렬

  ![Bubble Sort](https://github.com/Minho979/CS_Study/blob/main/contents/images/BubbleSort.gif)

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
  - 제자리 정렬(in-place sorting) 알고리즘으로 메모리가 절약된다
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
  - 두 번째 원소부터 시작해 그 앞의 원소들과 비교하여 삽입할 위치를 지정
    - 처음 Key 값: 두 번째 원소
  - 원소를 뒤로 옮기고 지정된 자리에 자료를 삽입
 
  ![InsertionSort](https://github.com/Minho979/CS_Study/blob/main/contents/images/InsertionSort.gif)

- 삽입 정렬 예시
  - 29, 10, 14, 37, 13이 저장된 배열을 오름차순으로 정렬

  ![InsertionSort](https://github.com/Minho979/CS_Study/blob/main/contents/images/InsertionSortEx.png)
 
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
  - 제자리 정렬(in-place sorting) 알고리즘으로 메모리가 절약
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
> - [정렬 알고리즘 6개 정리](https://jinhyy.tistory.com/9)
