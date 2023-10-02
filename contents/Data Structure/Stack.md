# Stack
## Stack의 개념

  ![Stack의 구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/Stack.png)

  - 한 끝에서만 자료를 삽입, 삭제할 수 있는 LIFO(Last In First Out) 형식의 자료 구조

## Stack의 연산
  - Stack은 LIFO를 따르기에 가장 최근에 스택에 추가한 항목이 가장 먼저 제거될 항목이다.
    - pop()`O(1)`: 스택에서 가장 위에 있는 항목을 제거한다.
    - push(item)`O(1)`: item 하나를 스택의 가장 윗 부분에 추가한다.
    - peek()`O(1)`: 스택의 가장 위에 있는 항목을 반환한다.
    - isEmpty()`O(1)`: 스택이 비어 있을 떄에 true를 반환한다.

## 순차 자료구조 Stack

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/LinearStack.png" width="500">

  - 1차원 배열을 이용하여 구현
  - 배열의 크기만큼 자료 저장 가능
  - 삽입/삭제 시 자료이동 오버헤드가 발생하지 않음
    - top에서만 삽입, 삭제가 이루어지기에 순차 자료구조임에도 자료이동 오버헤드가 존재하지 않음
  - 모든 연산 시간 복잡도는 O(1)
### 순차 자료구조 Stack의 장점
  - 1차원 배열을 통해 쉽게 구현 가능
  - 연산의 구현이 쉽고, 빠르게 수행
### 순차 자료구조 Stack의 단점
  - 스택 크기 변경의 비효율성
  - 빈 공간으로 메모리 낭비

## 연결 자료구조 Stack

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/LinkedStack.png" width="500">

  - 단순 연결 리스트를 이용하여 구현
  - 크기 변경에 자유로우며, 빈 공간으로 인한 메모리 낭비가 없음
  - 모든 연산 시간 복잡도는 O(1)

## Stack의 사용 사례
  - 재귀 알고리즘을 사용하는 경우에 유용
    - 재귀 알고리즘
      - 재귀적으로 함수를 호출해야 하는 경우에 임시 데이터를 스택에 넣어준다.
      - 재귀함수를 빠져 나와 퇴각 검색(backtrack)을 할 때는 스택에 넣어 두었던 임시 데이터를 빼 줘야한다.
      - 스택은 이러한 일련의 행위를 직관적으로 가능하게 해준다.
      - 또 스택은 재귀 알고리즘을 반복 형태(iterative)를 통해서 구현할 수 있게 해준다.
    - 시스템 스택
      - 프로그램의 호출과 복귀에 따른 순서를 관리
        - 가장 마지막에 호출된 함수가 가장 먼저 실행을 완료하고 복귀하는 LIFO 구조
        - 호출 발생 시 반환 주소 등을 스택 프레임(Stack Frame)에 저장하여 시스템 스택에 삽입
        - 실행 종료 후 시스템 스택의 top 원소(스택 프레임)을 삭제하면서 프레임에 저장된 주소로 복귀
        - 해당 과정을 반복하여 전체 프로그램이 종료되면 시스템 스택은 공백이 됨
    - 웹 브라우저 방문기록(뒤로가기)
    - 실행 취소(undo)
    - 역순 문자열 만들기
    - 수식의 괄호 검사(연산자 우선순위 표현을 위한 괄호 검사)
      - 예) 올바른 괄호 문자열(VPS, Valid Parenthesis String) 판단하기
    - 후위 표기법 계산

> ⬆️:[Top](#Stack)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#1-data-structure)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [이지영. 지바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [[자료구조] 스택(Stack)이란](https://gmlwjd9405.github.io/2018/08/03/data-structure-stack.html)
