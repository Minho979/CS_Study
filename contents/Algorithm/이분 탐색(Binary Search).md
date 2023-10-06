# 이분 탐색(Binary Search)
## 개념
- 정렬되어 있는 리스트에서 탐색 범위를 절반씩 좁혀가며 데이터를 탐색하는 알고리즘
- 배열 내부의 데이터가 정렬되어 있는 경우에만 사용할 수 있음
- `start, mid, end` 3개의 변수를 사용하여 탐색을 진행
  - 찾으려는 데이터와 중간점 위치에 있는 데이터를 반복적으로 비교하며 탐색

## 원리
1. 배열의 중간 값(mid)를 설정
   - 배열이 정렬되어 있으므로 중간 인덱스의 값
2. mid 값과 검색 값을 비교한다
   1. `mid = target` 검색 종료
   2. `mid < target` start를 `mid +1` 로 설정하여 오른쪽 구간 탐색
   3. `mid > target` end를 `mid -1`로 설정하여 왼쪽 구간 탐색
3. 값을 찾거나 'start > end'가 될 때까지 반복
   - 'start > end'인 경우 해당 배열에 찾는 데이터가 없는 것

![Binary Search vs Linear Search](https://github.com/Minho979/CS_Study/blob/main/contents/images/binary-and-linear-search-animations.gif)

## 시간 복잡도
- 각 단계마다 탐색 범위를 절반으로 나누기에 $O(logn)$
- 순차 탐색의 경우 배열의 모든 원소를 확인해야할 수 있기에 $O(n)$

## 장점
- 배열이 정렬되어 있는 경우 빠른 속도의 탐색시간을 보장함

## 단점
- 정렬되어 있지 않은 배열에는 사용할 수 없음

## 구현 코드
### 반복문 구현
``` java
public static int binarySearch(int[] a, int target) {
		int start = 0;
		int end = a.length -1;
		int mid;
		
		while(start <= end) {
			mid = (start + end)/2;
			if (a[mid] < target) {
				start = mid + 1;
			}
			else if (a[mid] > target) {
				end = mid -1;
			}
			else {
				return a[mid];
			}
		}
		return (Integer) null;
	}
```
### 재귀호출 구현
``` java
public static int binarySearchRecursive(int[] a, int start, int end, int target) {
		if (start > end) {
			return (Integer) null;
		}
		
		int mid = (start + end)/2;
		
		if (a[mid] < target) {
			return binarySearchRecursive(a, mid +1, end, target);
		}
		else if(a[mid] > target) {
			return binarySearchRecursive(a, start, mid -1, target);
		}
		else {
			return a[mid];
		}
		
	}
```

> ⬆️:[Top](#이분-탐색Binary-Search)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [[알고리즘] 이분 탐색 / 이진 탐색 (Binary Search)](https://velog.io/@kimdukbae/%EC%9D%B4%EB%B6%84-%ED%83%90%EC%83%89-%EC%9D%B4%EC%A7%84-%ED%83%90%EC%83%89-Binary-Search)
> - [[알고리즘/Java] 이분 탐색 / 이진 탐색 (Binary Search)](https://velog.io/@suk13574/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%9D%B4%EB%B6%84-%ED%83%90%EC%83%89-%EC%9D%B4%EC%A7%84-%ED%83%90%EC%83%89-Binary-Search)
