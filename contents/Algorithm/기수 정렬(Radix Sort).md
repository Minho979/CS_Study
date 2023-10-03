# 기수 정렬(Radix Sort)
## 개념
  - 비교 연산을 수행하지 않아 조건이 충족하는 상황이라면 매우 빠른 속도를 보장
  - 데이터의 각 자리수를 낮은 자리수부터 가장 큰 자리수까지 차례대로 올라가며 정렬
  - 기수에 따른 추가 버킷 공간이 필요
    - Ex) 10진수 -> 기수 10 -> 버킷 10개 요구
    - 버킷: 기수만큼 Queue를 이용해 만든 저장공간
    - [큐(Queue)란?](https://github.com/Minho979/CS_Study/blob/main/contents/Data%20Structure/Queue.md)
  - 안정정렬
 
## 기수 정렬 과정

  1\. 현재 데이터들 중 가장 큰 자리수를 파악
  
  2\. 각 데이터들의 1의 자리를 비교하여 오름차순 정렬
  
  3\. 그 뒤 10의 자리수를 비교하여 오름차순 정렬
  
  4\. 3번의 과정에서 10의 자리가 없다면 0으로 간주
  
  5\. 위의 과정을 가장 큰 자리수까지 반복

### 예시
  
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

## 시간 복잡도
  - 정렬할 원소의 수(n), 가장 긴 값의 자리수(d), 버킷 수를 결정하는 기수(r)의 영향을 받음
  - 정렬할 원소 n개를 r개의 버킷에 분배하고 다시 꺼내 합치는 작업: $O(n+r)$ 
  - 위의 작업을 자리수 d만큼 반복하므로 $O(d(n+r))$
  - d와 r의 경우 n에 비하면 상수라 봐도 무관함
  - 모든 경우에서 $O(n)$

## 공간 복잡도
  - 기수만큼의 버킷 공간을 요구하기에 $O(n+r)$
  - r은 기수의 크기이기에 n에 비해 무시할 수 있는 상수로 볼 수 있음
  - $O(n)$

## 장점
  - 자리수의 값을 비교하여 정렬하는 방식이기에 문자열, 정수 등을 빠른 속도로 정렬 가능
  - 동일 값이 있어도 변하지 않는 안정정렬(Stable Sort)
  - 시간 복잡도는 $O(n)$으로 매우 빠른 수행 속도를 보장

## 단점
  - 적용할 수 있는 범위가 제한적
    - 아스키 코드로 표현 가능한 정수, 알파벳, 특수문자 등은 가능하지만 소수는 불가능함
  - 기수만큼의 추가 메모리 공간(버킷 공간)을 요구함
    - 비 제자리 정렬(out of place sort) 
  - 버킷의 크기를 모든 케이스에 알맞게 정의하기 어려움
 
## 구현 코드
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

> ⬆️:[Top](#기수-정렬Radix-Sort)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [이지영. 자바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [[JAVA] 기수 정렬 (Radix Sort)](https://banjjak1.tistory.com/52)
