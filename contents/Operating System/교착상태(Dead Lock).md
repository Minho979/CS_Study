# 교착상태(Dead Lock)
## 교착상태의 개념
- 다중 프로그래밍 시스템에서 프로세스들이 한정된 시스템 자원을 차지하기 위해 경쟁할 때 생기는 문제 중 하나로 작업을 수행하지 못하고 기다리기만 하는 상태를 말한다.
- 결코 일어나지 않을 사건(event)을 프로세스가 기다리고 있는 상태를 말한다.
- 교착상태의 가능성이 있을 뿐, 상대적인 속도에 의해 교착상태가 발생하지 않을 수도 있고 발생할 수도 있다.

### 교착 상태가 시스템에 미치는 영향
- 자원 요구가 뒤엉켜 교착상태에 빠진 프로세스들은 반납되지 않을 자원을 기다리므로 작업을 더 이상 진행할 수 없다.
- 운영체제가 교착상태를 해결하지 못하는 경우 시스템 운영자나 사용자가 프로그램 종료 등의 방법으로 해결해야한다. 

### 프로세스의 자원 이용 순서
1. 요청: 프로세스가 필요한 자원을 요청하는 단계
    - 요청이 받아들여지면 자원을 할당 받는다.
    - 요청이 즉시 받아들여지지 않는 경우 다른 프로세스가 해당 자원을 사용 중인 것으로 할당 받을 때까지 대기한다.
   
2. 사용: 프로세스가 요청한 자원을 점유하여 사용하는 단계
   
3. 해제: 프로세스가 자원 사용을 마친 후 자원을 반납하는 단계
- 자원의 요청과 해제는 시스템 호출(System call)을 통해 수행한다. 

## 교착상태의 예시

#### 일상 생활의 예시
  - 차량들이 교차로를 통과하지 못하고 멈춘 교통 마비 상태

    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-ex1.png' width='500'>
    
#### 스플링 시스템 교착상태
  - 출력을 시작하기 전에 출력물을 디스크 스풀링 파일에 완전히 내보내야하는 경우, 완료된 작업이 없는데 중간에 스풀링 공간이 모두 차버린 교착상태를 말한다.
  - 예) P1: 스풀링 공간 요구량 10, P2: 스풀링 공간 요구랑 10, 스풀링 공간: 15  
    P1: 스풀링 공간 7 사용, P2: 스풀링 공간 8 사용으로 전체 스풀링 공간이 가득차 두 프로세스 모두 작업 완료가 불가능한 교착상태가 발생할 수 있다.

  - 해결책
    - 필요량보다 많은 스풀링 공간을 배당
      - 비용이 많이 들어가는 단점이 있다.
    - 포화 임계치(saturation threshold)를 설정
      - 시스템 처리량이 줄어들 수 있다는 단점이 있다.
      - 예) 포화 임계치 75%인 경우 스풀링 공간의 75%가 차면 새로운 작업이 들어올 수 없다.
  - 현대 시스템의 해결책
    - 출력물을 전부 내보내기 전에 출력을 시작할 수 있게 하여 가득찬 스풀링 파일을 비울 수 있게 한다.
    - 스풀링 공간을 동적으로 할당한다. 

#### 네트워크에서 발생하는 교착상태
- 네트워크가 붐비거나 입출력 버퍼 공간이 부족한 네트워크 시스템에 메세지 흐름을 제어하는 적절한 프로토콜이 없는 경우 교착 상태가 발생할 수 있다.

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-ex2.png' width='500'>

#### 장치 할당 요구시 교착상태
- 이미 할당된 장치를 요청한 경우 어떠한 프로세스도 요청 장치를 할당 받지 못해 작업을 완료할 수 없는 교착 상태에 빠질 수 있다.

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-ex3.png' width='500'>
  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-ex4.png' width='500'>

    - A는 B의 자원을 기다리고, B는 A의 자원을 기다린다.
    - 위의 경우 B가 CD레코더를 반납해야 교착상태를 해결할 수 있으나 B는 스캐너를 할당 받아 작업을 완료해야 반납할 수 있다.
    -  즉, 상대방이 미리 가지고 있는 자원의 요청이 있는 경우 거절하기에 발생하는 문제이다. 

## 교착상태의 발생 조건
아래의 모든 조건을 만복할 때 교착상태가 발생할 수 있다.  
교착상태는 무조건 적으로 발생하는 것이 아니라 상대적인 속도에 의해 발생하지 않을 수도 있다.

- 상호 배제(mutual exclusion)
  - 한 번에 한 프로세스만 해당 자원을 사용할 수 있다.
  - 만약 여러 프로세스가 사용이 가능하다면 교착상태가 형성되지 않는다.
- 점유와 대기(hold and wait)
  - 최소 자원 하나를 가지고 다른 프로세스에 할당된 자원을 얻기 위해 기다린다.
- 비선점(no-preemption)
  - 자원은 선점될 수 없다. 즉, 자원을 강제로 뺏을 수 없으며 자원을 점유하고 있는 프로세스가 자원 사용을 마쳐야 해제된다.
  - 실행 중에는 중단이 불가능하다.
  - 중단 후 다시 이어서 사용이 가능한 자원은 교착상태를 형성할 수 없다. 
- 순환대기(circular wait)
  - 대기 프로세스 집합 {P0, P1, ..., Pn-1}이 있을 때, P0은 P1이 점유하고 있는 자원을, P1은 P2가 점유하고 있는 자원을, ... Pn-1은 P0이 점유하고 있는 자원을 대기하여 점유-대기 관계가 사이클을 형성한다.

    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-circular-wait.png' width='300'>

- 강 건너기 예로 살펴본 교착상태의 조건

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-bridge.png' width='500'>
  
  - mutual exclusion(상호배제):  한 번에 한 사람만 지나갈 수 있음
  - hold and wait(점유와 대기): 발판이라는 자원을 가진채로 다음 발판을 대기 중
  - no-preemption(비선점): 중단 불가, 후진 불가능, 다리를 건너야 끝이남
  - circular wait(순환대기): 서로 점유를 가지고 서로 요청한 자원(상대가 점유한 자원)대기

## 교착상태의 표현
### 자원 할당 그래프
- 자원 할당 그래프의 사이클 존재 유무를 통해 교착상태를 알아낼 수 있다.
- 어떤 자원과 어떤 프로세스가 교착상태에 연관 되어있는지를 알 수 있다.
- 같은 유형의 자원이 여러 개인 경우 사이클이 없으면 교착상태가 아니지만 사이클이 있는 경우 교착상태일 수도 있고 아닐 수도 있다.
- 자원 할당-요청 관계를 나타낸 방향 그래프 G = (V, E)
  - 정점 집합 V: 프로세스(Pi)와 자원(Rj)
  - 간선 집합 E: <Pi, Rj> 요청 연결선과 <Rj, Pi> 할당 연결선

    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-request.png' width='300'>
    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-allocation.png' width='300'>

#### 자원 할당 그래프를 이용한 교착 상태 표현
- 자원 할당 그래프에 사이클이 존재하는 경우
  - 사이클을 구성하는 프로세스와 자원이 교착상태에 연관되어 있음을 나타낸다.
 
  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-resource-allocation-graph.png' width='500'> 

#### 같은 유형의 자원이 여러 개인 경우 자원 할당 그래프 예
- 사이클이 있으며 교착상태인 예
  
  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-resource-allocation-graph-ex1.png' width='500'>
  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-resource-allocation-graph-ex2.png' width='500'>

- 사이클이 있으나 교착상태가 아닌 예

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-resource-allocation-graph-ex3.png' width='500'>

  - P2가 R1을 사용하고 R1 반납 → R1이 P1에 할당 → 사이클이 사라짐 → 교착상태 발생 X
## 교착상태의 해결 방법

> ⬆️:[Top](#교착상태Dead-Lock)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Operating-System)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [구현회. 운영체제-그림으로 배우는 구조와 원리, 개정3판. 한빛아카데미]
