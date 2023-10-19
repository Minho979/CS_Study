# 동적 프로그래밍(Dynamic Programming)
- 동적 프로그래밍(DP)은 특정 문제에 있어 심한 중복 호출이 발생하여 재귀적 구현이 매우 비효율적인 경우를 해결하기 위해 등장
- DP는 기본적으로 큰 문제를 여러 개의 작은 문제로 나누어 수행의 결과를 저장하여 필요할 때 다시 사용하여 큰 문제를 해결하는 일종의 문제해결 패러다임

## 동적 프로그래밍의 적용 조건
아래의 두 가지 조건을 모두 만족해야 한다.
1. 최적 부분구조(Optimal Substructure)
   - 큰 문제의 최적 솔루션에 작은 문제의 최적 솔루션이 포함된 경우
   - 작은 문제의 결과 값을 통해 큰 문제의 최적 솔루션이 도출 가능한 경우
   - 해당 특성에 의해 특정 문제의 솔루션은 문제의 크기에 상관없이 항상 동일
2. 재귀 호출시 중복(Overlapping Recursive Calls)
   - 재귀적 구현시 같은 문제에 대한 재귀 호출이 심하게 중복되는 경우(동일한 부분 문제가 반복하여 등장하는 경우)
   - 재귀 호출로 얻은 결과를 사용할 수 있는 부분 문제가 반복적으로 등장하지 않을 경우 재사용이 불가능하여 사용 불가

## 동적 프로그래밍의 구현
1. Top-Down 방식
   - 재귀적으로 구현하되, 호출된 적이 있으면 메모해두어 중복 호출 문제를 해결하는 방법 (Memoization)
     - 함수의 앞 부분에 이미 해결된 적이 있는 문제인지 확인하는 부분을 두어 해결된 문제이면 저장된 값을 리턴
   - 가독성이 좋지만 StackOverflow 에러가 발생할 수 있음
2. Bottom-Up 방식
   - 아래에서부터 계산을 수행하고 누적시켜 전체의 큰 문제를 해결하는 방법 (Tabulation)
   - 더 흔히 사용됨
   - 해결이 용이하지만 가독성이 떨어질 수 있음

### 재귀, Top-Down, Bottom-Up 비교
- 재귀를 이용하여 구현한 피보나치 수열의 경우 $O(2^n)$
- DP를 이용하여 Bottom-Up으로 구현한 피보나치 수열의 경우 $O(n)$
- Top-Down의 경우 호출의 빈도를 현저하게 줄여줌
#### 재귀 호출로 구현한 피보나치 수열
``` java
public static int fib(int n) {
    if (n <= 1) {
      return n;
    }
    else {
      return fib(n - 1) + fib(n - 2);
    }
}
```
    
#### Bottom-Up 방식으로 구현한 피보나치 수열
``` java
public class BottomUpFib {
    static int[] f = new int[10];
 
    static int fib(int n) {
        f[1] = f[2] = 1;
        for (int i = 3; i <= n; i++) {
            f[n] = f[n - 1] + f[n - 2];            
        }
        return f[n];
    }
}
```

#### Top-Down 방식으로 구현한 피보나치 수열
``` java
public class TopDownFib {
    static int[] f = new int[1000];
 
    static int fib(int n) {
        if (n == 1 || n == 2) {
            return 1;
        }
        else if (f[n] > -1) {
            return f[n];
        }
        else {
            f[n] = fib(n - 2) + fib(n - 1);
            return f[n];
        } 
    } 
}
```

#### 재귀, Top-Down Call Tree 비교
- Top-Dwon이 재귀적으로 동작하지만 동일한 문제의 중복 호출 문제가 없는 것을 볼 수 있다
#### 재귀 호출로 구현한 피보나치 수열의 Call Tree
<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/RecursiveFib.png" width="500">

#### Top-Down 방식으로 구현한 피보나치 수열의 Call Tree
<img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/TopDownFib.png" width="500">

## 동적 프로그램 적용 과정
1. DP로 풀 수 있는 문제인지 확인
   - 두 가지 조건을 충족하는 문제인지 체크
2. 문제의 변수 파악
   - 문제 내의 변수의 개수를 파악
3. 변수 간의 관계식(점화식) 만들기
4. 메모하기(Memoization or tabulation)
   - 변수 값에 따른 결과를 저장
5. 기저 상태 파악하기
    - 가장 작은 문제의 상태 파악
6. 구현하기

## 동적 프로그래밍의 예
- [행렬 경로 문제](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%ED%96%89%EB%A0%AC%20%EA%B2%BD%EB%A1%9C%20%EB%AC%B8%EC%A0%9C.md)
- [돌 놓기 문제](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EB%8F%8C%20%EB%86%93%EA%B8%B0%20%EB%AC%B8%EC%A0%9C.md)
- [행렬 곱셈 순서 문제](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%ED%96%89%EB%A0%AC%20%EA%B3%B1%EC%85%88%20%EC%88%9C%EC%84%9C%20%EB%AC%B8%EC%A0%9C.md)
- [최장 공통 부분수열(LCS)](https://github.com/Minho979/CS_Study/blob/main/contents/Algorithm/%EC%B5%9C%EC%9E%A5%20%EA%B3%B5%ED%86%B5%20%EB%B6%80%EB%B6%84%EC%88%98%EC%97%B4(LCS).md)

> ⬆️:[Top](#동적-프로그래밍Dynamic-Programming)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Algorithm)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
> - [알고리즘 - Dynamic Programming(동적 계획법)](https://hongjw1938.tistory.com/47)
