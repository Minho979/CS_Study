# 2. Algorithm

#### Contents
- [알고리즘(Algorithm)](#알고리즘Algorithm)
- [시간복잡도(Time Complexity)와 공간복잡도(Space Complexity)](#시간복잡도Time-Complexity와-공간복잡도Space-Complexity)
- [선택 정렬(Selection Sort)](#선택-정렬Selection-Sort)


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

