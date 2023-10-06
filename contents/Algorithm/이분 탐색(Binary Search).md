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

## 시간 복잡도
- 각 단계마다 탐색 범위를 절반으로 나누기에 $O(logn)$
- 순차 탐색의 경우 배열의 모든 원소를 확인해야할 수 있기에 $O(n)$

## 장점
- 배열이 정렬되어 있는 경우 빠른 속도의 탐색시간을 보장함

## 단점
- 정렬되어 있지 않은 배열에는 사용할 수 없음

## 구현 코드
``` java
```

> ⬆️:[Top](#이분-탐색Binary-Search)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [[알고리즘] 이분 탐색 / 이진 탐색 (Binary Search)](https://velog.io/@kimdukbae/%EC%9D%B4%EB%B6%84-%ED%83%90%EC%83%89-%EC%9D%B4%EC%A7%84-%ED%83%90%EC%83%89-Binary-Search)
> - [[알고리즘/Java] 이분 탐색 / 이진 탐색 (Binary Search)](https://velog.io/@suk13574/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EC%9D%B4%EB%B6%84-%ED%83%90%EC%83%89-%EC%9D%B4%EC%A7%84-%ED%83%90%EC%83%89-Binary-Search)
