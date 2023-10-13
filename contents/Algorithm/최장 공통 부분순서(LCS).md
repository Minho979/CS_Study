# 최장 공통 부분순서(LCS: Longest Common Subsequence)
- 두 문자열에 공통적으로 들어있는 공통 부분순서 중 가장 긴 문자열
- 최장 공통 문자열(Longest Common Substring) 또한 LCS라고 불림
- 최장 공통 문자열의 경우 최장 공통 부분순서를 구하는데 사용 됨

## 용어 정리
### Subsequence
- 문자열의 부분순서로 이어지지 않고 떨어져 있어도 되지만 순서는 뒤바뀌어서는 안됨
- \<bcdb\>는 문자열 \<abcbdab\>의 subsequence

### Common subsequence
- 두 문자열의 공통 부분순서
- \<bca\>는 문자열 \<abcbdab\>와 \<bdcaba\>의 common subsequence

### Longest Common Subsequence(LCS)
- 두 문자열의 최장 공통 부분순서 (Common subsequence 중 가장 긴 것)
- \<bcba\>는 문자열 \<abcbdab\>와 \<bdcaba\>의 LCS(Longest Common Subsequence)

### Longest Common Substring(LCS)
- 두 문자열의 최장 공통 문자열로 한번에 이어져있는 문자열
- \<ab\>, \<bd\>는 문자열 \<abcbdab\>와 \<bdcaba\>의 LCS(Longest Common Substring)

## 최장 공통 문자열(Longest Common Substring)
### 재귀 알고리즘
``` java
LCS(i, j) {
    if (i == 0 || j == 0)  // 마진 설정
        return 0;
    // 이전 문자열의 값에 +1 
    else if (string _A[i] == string _B[j]) 
        LCS[i, j] = LCS[i - 1, j - 1] +1;
        return LCS[i, j]
    // 연속성을 위해 같지 않다면 0
    else
        return 0;
}
```
- 공통 문자열은 연속되어야 하기에 두 문자의 앞 글자까지가 공통 문자열이라면 계속 문자열이 이어지고 아니라면 본인부터 공통 문자열을 생성

### 수행 과정
1. 문자열 A, 문자열 B의 한글자씩 비교
2. 두 문자가 다르다면 LCS[i][j]에 0을 표시
3. 두 문자가 같다면 LCS[i - 1, j - 1] 값을 찾아 +1
4. 위 과정을 반복

#### 수행 과정 예시 

## 최장 공통 부분순서(Longest Common Subsequence)

## 최적 부분구조의 재귀적 관계
- 두 문자열 $A_m$ = < $a_1a_2...a_m$ >과 $B_n$ = < $b_1b_2...b_n$ >에 대해
  -  $a_m$ = $b_n$이면, $A_m$과 $B_n$의 LCS 길이는 $A_{m-1}$과 $B_{n-1}$의 LCS의 길이보다 1이 크다
  -  $a_m$ != $b_n$이면, $A_m$과 $B_n$의 LCS 길이는 $A_m$과 $B_{n-1}$의 LCS 길이와 $A_m$과 $B_n$의 LCS 길이는 $A_{m-1}$과 $B_n$의 길이 중 큰 것과 같다

### 문제 정의(점화식)
$c_{ij}$: 두 문자열 $A_m$ = < $a_1a_2...a_m$ >과 $B_n$ = < $b_1b_2...b_n$ >의 LCS 길이
- $c_{ij}$ = 0
  - `if i = 0 or j = 0`
- $c_{ij}$ = $c_{i-1, j-1} + 1$
  - `if i, j > 0 and a_i == b_j`
- $c_{ij}$ = max ($c_{i-1, j},c_{i, j-1}$)
  - `if i, j > 0 and a_i != b_j`
- 최종적으로 $c_{mn}$이 답

## 알고리즘 
### 재귀 알고리즘
``` java
LCS(m. n) {
    if (m == 0 || n == 0)
        return 0;
    else if (string _A[m] == string _B[n])
        LCS[m, n] = LCS[m - 1, n - 1] +1;
        return LCS[m, n]
    else
        return max(LCS[m - 1, n], LCS[m, n - 1]);
}
```
- 엄청난 중복 호출 발생

### 재귀 알고리즘 Call-Tree

### 재귀 알고리즘 호출 횟수 

### DP 알고리즘
``` java
/*
string _A[m]과 string _B[n]의 LCS 길이를 구한다
C[i, j]: C[0...m][0...n] string _A[m]과 string _B[n]의 LCS 길이를 저장
         부분 문제의 답을 저장
*/
LCS(m. n) {
    for (int i = 0; i < m; i++) {
        C[i, 0] = 0;
    }
    for (int j = 0; j < n; j++) {
        C[0, j] = 0;
    }
    for (int i = 1; i < m; i++) { 
        for (int j = 1; j < n; j++) {
            if (string _A[i] == string _B[j])
                C[i, j] = C[i - 1, j - 1] +1;
            else
                C[i, j] = max(C[i - 1, j], C[i, j - 1]);
        }
    }
    return C[m, n]
}
```

## 수행 과정
간단한 설명을 위해 재귀 알고리즘을 사용하여 예시를 설명
1. 문자열 A, 문자열 B의 한글자씩 비교
2. 두 문자가 다르다면 LCS[m - 1, n], LCS[m, n - 1] 중 큰 값을 표시
3. 두 문자가 같다면 LCS[m - 1, n - 1] 값을 찾아 +1
4. 위 과정을 반복

- LCS[m - 1, n], LCS[m, n - 1]의 의미
  - 부분순서는 연속된 값이 아니기에 현재 문자를 비교하는 과정 이전의 최대 공통 부분순서가 계속해서 유지되기에 LCS[m - 1, n], LCS[m, n - 1]는 이전 과정에 해당
- 문자가 같은경우 LCS[m, n] = LCS[m - 1, n - 1] +1인 이유
  - 두 문자가 같은 상황인 경우 지금까지의 최대 공통 부분순서에 1을 더해주는 것
  - LCS[m - 1, n], LCS[m, n - 1]의 LCS 배열은 비교를 통해 언제나 최대 공통 부분순서의 값을 가지고 있음

### 수행 과정 예시

## 최장 공통 부분순서(Longest Common Subsequence) 찾기 
경우에 따라 여러가지의 답이 나올 수 있으나 한가지 경우만을 보는 예시

### 수행 과정
1. LCS 배열의 가장 마지막 값에서 시작, 결과값을 저장할 result 배열을 준비
2. LCS[m - 1, n], LCS[m, n - 1] 중 현재 값과 같은 값을 탐색
   2-1. 만약 같은 값이 있다면 해당 값으로 이동
   2-2. 만약 같은 값이 없다면 result 배열에 해당 문자를 넣고 LCS[m - 1, n - 1]로 이동
3. 2번 과정을 반복하다 0으로 이동하면 종료, result 배열의 역순이 LCS

#### 수행 과정 예시

> ⬆️:[Top](#최장-공통-부분순서LCS-Longest-Common-Subsequence)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [[알고리즘] 그림으로 알아보는 LCS 알고리즘 - Longest Common Substring와 Longest Common Subsequence](https://velog.io/@emplam27/%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-%EA%B7%B8%EB%A6%BC%EC%9C%BC%EB%A1%9C-%EC%95%8C%EC%95%84%EB%B3%B4%EB%8A%94-LCS-%EC%95%8C%EA%B3%A0%EB%A6%AC%EC%A6%98-Longest-Common-Substring%EC%99%80-Longest-Common-Subsequence)
