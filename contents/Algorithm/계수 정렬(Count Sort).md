# 계수 정렬(Count Sort)
## 개념
  - 비교 연산을 사용하지 않고, 배열 내에서 특정 값이 등장하는 횟수를 통해 정렬을 수행

## 제약 사항
  - 데이터 값은 양수
  - 데이터 값의 범위가 O(n) 범위에 있을 때 사용 가능
    - 값의 범위가 메모리 사이즈가 넘지 않도록 너무 크지 않아야 함

## 계수 정렬 과정

  1\. 입력 받은 배열 A의 요소 값의 등장 횟수를 카운팅할 배열 Count와 최종적으로 정렬된 값을 담을 배열 B를 설정

  2\. 배열 A에서 값을 하나씩 꺼내 해당 값을 Count의 인덱스로 사용해 Count의 요소 값을 하나 증가
     
    Count[A[i]]++
  
  3\. Count가 완성되면 Count의 각 요소들을 누적합으로 합산
     
    Count[i] = Count[i] + Count[i-1]
  
  4\. A의 가장 뒤에서부터 값을 꺼내 해당 값을 Count의 인덱스로 사용하고 참조된 B의 값을 하나 감소
     
    Count[A[i]]--
  
  5\. 감소된 B의 값을 C의 인덱스로 사용해 A에서 꺼낸 값을 삽입
     
    B[Count[A[i]]] = A[i]
  
  6\. A의 모든 요소에 대해 4번 5번 과정을 반복한다 

### 예시

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


## 시간 복잡도
  - Count 배열 생성에 필요한 시간 $O(n)$
  - Count 배열 뒤에서부터 순회하여 값을 채우는 시간 $O(n)$
  - 최악의 경우 $O(n+k)$
    - k는 음이 아닌 키 값의 범위를 의미
  - $O(n)$
    - Why? n에 비하면 k의 값은 상수로 보아도 무관

## 공간 복잡도
  - 추가적인 배열을 생성하기에 $O(n)$

## 장점
  - 비교 연산이 없어 빠른 수행시간 $O(n)$을 보장
    - 해당 성능을 보장하기 위해서는 데이터의 명확한 제한이 필요
  - 안정 정렬(Stable Sort)

## 단점
  - 정렬을 하기 위한 추가적인 메모리가 필요
  - 카운팅을 하기 위한 배열의 길이가 최대값에 의해 결정되어 메모리 낭비가 발생할 수 있음
  - 데이터의 수보다 배열의 크기가 클 경우 비효율적
    - (1, 10000) 두 개의 값만 가지더라도 Count 배열의 크기는 10001
  - 음수가 섞인 경우 사용 불가하며 명확한 데이터 제한이 필요
 
## 구현 코드
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

> ⬆️:[Top](#계수-정렬Count-Sort)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [알고리즘 6일차 - O(n) 정렬, 계수 정렬](https://velog.io/@chappi/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-6%EC%9D%BC%EC%B0%A8-On-%EC%A0%95%EB%A0%AC-%EA%B3%84%EC%88%98-%EC%A0%95%EB%A0%AC)
