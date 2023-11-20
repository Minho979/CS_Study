# 교착상태(DeadLock)
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
### 교착상태 예방(DeadLock Prevention)
- 교착상태가 절대 일어나지 않도록 방지하는 방법이다.
- 명쾌하지만 자원 활용도가 떨어진다.
- 교착상태 필요 조건 4가지 중 하나만 방지하더라도 교착상태를 예방할 수 있다.
  - 교착상태는 한 순간 하나의 프로세스만 이용 가능한 자원에서 생기는 문제로 상호배제를 통한 예방은 불가능하며 무의미하다.
#### hold and wait 조건 방지
**원리**
- 자원을 점유한 프로세스가 추가 자원 요청을 할 수 없도록하여 프로세스가 자원을 점유한 채로 다른 자원을 기다리는 일을 없애는 방식이다.
  
**방법**
1. 각 프로세스는 필요한 자원을 한번에 요청해야 하며, 요청한 자원을 모두 할당 받기 전까지는 작업을 진행할 수 없다.
2. 자원을 추가 요청하기 전에 점유 중인 모든 자원을 일단 해제한 후 요청할 수 있다.
  
**단점**
- 자원 사용 효율이 낮아진다.
  - 많은 자원이 사용되지 않으면서 오랜 시간 할당되어 있어 효율이 낮아진다.
- 기아상태가 발생할 수 있다. (대화식 시스템에서 사용이 불가능하다.)
  - 자주 이용하는 자원이 다른 프로세스에 할당된 경우, 이 자원을 요청한 프로세스는 모든 자원이 동시에 빌 때까지 무기한 기다려야 하는 경우가 발생할 수 있다.
  - 적은 수의 자원을 요청한 프로세스가 유리하므로, 많은 수의 자원을 요청한 프로세스의 대기시간이 길어질 수 있다.

#### no-preemption 조건 방지
**원리**
- 프로세스가 점유한 자원을 강제로 해제할 수 있도록 하는 방법이다.
  
**방법**
1. 어떤 자원을 점유한 프로세스가 추가 자원 요청시 기다려야 한다면, 프로세스는 현재 점유한 자원을 모두 해제한다.
2. 자원 해제를 줄이기 위해 R1을 점유한 P1이 요청한 R2를 P2가 점유하고 있다면 P2가 실행 중인지 대기 중인지를 검사한다.
      - P2가 대기중인 경우 R2를 빼앗아 P1에 할당한다.  
      - P2가 실행 중인 경우 P1은 대기하며 만일 P2가 R1을 요청할 경우 P1에게서 R1을 해제한다.
3. 프로세스에 우선순위를 부여하여 높은 우선순위의 프로세스가 그보다 낮은 순위의 프로세스가 점유한 자원을 빼앗을 수 있도록 한다.

**단점**
- 사용이 제한적이다.
  - 작업 상태를 쉽게 저장 및 복구 가능할 때만 사용이 가능하다.
    - 프린터, 테이프 드라이브 등과 같은 자원에는 적용이 불가능하다.
  - 자원 해제가 필요한 상황이 빈번하게 발생하지 않을 때만 이용이 가능하다.

#### circular wait 조건 방지
**원리**
- 특정 순서대로만 자원을 요청하게 만들어 자원 할당 그래프에 사이클이 형성되지 않도록 한다.

**방법**
1. 모든 자원에 일련의 순서(번호)를 부여하고, 각 프로세스는 이 번호 오름차순으로만 자원을 요청하도록 한다.  
  즉, 자원 Ri를 요청한 후에는 이보다 번호가 높은 자원 Rj만 요청이 가능하다.

   <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-prevention.png' width='300'>

    - P3가 R3 → R0의 순서로 필요로 할 경우 R3, R0 순서로 요청이 불가능하고 R0, R3 순서로 요청을 해야한다.
    
3. 자원 Rj를 요청할 때, 이보다 번호가 높은 자원을 해제한다.

- 예) 함수 F: R → N의 예
  - 자원 집합 R = {R1, R2, ..., Rn}, 자연수 집합 N
  - F(CD 드라이브) = 3, F(디스크 드라이브) = 4, F(프린터) = 7
  - 7을 할당 받은 상태로 4를 요청할 수 없다.
  - 만약 프린터와 CD가 동시에 필요할 때 프린트 중 CD 이용이 불가능하다.
    - 이 경우 CD를 먼저 요구하여 미리 할당 받은 후 7을 사용하다 3을 이용한다. 
    
**단점**
- 주어진 순서와 다르게 자원을 필요로 하는 프로세스에서 자원이 낭비된다.
- 번호 부여시 실제로 자원을 사용하는 순서를 반영해야하는 부담이 있다.

### 교착상태 회피(DeadLock Avoidance)
- 시스템 내 교착상태 가능성이 존재하지만 회피 알고리즘을 통해 교착상태를 회피하지만 회피 알고리즘 실행으로 인해 시스템 부하가 가중된다.
  - 회피 알고리즘은 프로세스가 자원을 요청할 때마다 수행해야한다.
- 가용 자원이 충분히 있는 경우에도 자원 할당 시 교착상태가 발생할 위험이 있는 경우 요청을 거절한다.
- 교착상태 예방(deadlock prevention)보다 덜 엄격한 조건을 요구함으로써 자원을 더 효율적으로 이용하고, 병행성을 더 허용한다.
- 교착상태 회피를 위해 자원 요구에 대한 추가 정보가 필요하다.
  - 자원 할당 상태: 사용 가능한 자원의 수, 할당된 자원의 수, 프로세스들의 최대 요구 수에 의해 정의

#### 자원 할당 그래프 알고리즘(resource allocaion graph algorithm)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-Avoidance-resource-allocaion-graph-algorithm1.png' width='500'>
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-Avoidance-resource-allocaion-graph-algorithm2.png' width='500'>
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-Avoidance-resource-allocaion-graph-algorithm3.png' width='500'>

claim: 요구를 한 것이 아니라 실행 중에 요구할 계획이 있음을 알리는 것

#### 시스템의 두 가지 상태(안정 상태(stable state)와 불안정 상태(unstable state)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-Avoidance-state.png' width='500'>

**안정 상태(stable state)**
- 프로세스의 안정 순서가 존재하는 상태로 교착상태가 절대 발생할 수 없다.
- 각 프로세스에 자원을 최대 요구 수까지 할당할 수 있어 교착상태를 회피할 수 있는 상태이다.
- 프로세스 Pi가 필요한 자원을 즉시 사용할 수 없다면, Pi는 모든 Pj가 끝날 때까지 기다렸다가 자원을 확보하며, 필요한 모든 자원 확보 시 작업을 완료하고 자원을 반납한다.
- 어떤 시점에 시스템이 안정 상태임을 보이려면 안정 순서가 존재함을 보이면 된다.
  - 안정 순서: 그 시점부터 시작해 최악의 경우에도 모든 프로세스들이 작업을 완료할 수 있는 프로세스 순서
  - 프로세스 순서<P1, P2, ..., Pn>이 안정 순서라는 뜻은 Pi의 최대 자원 요청이 두 가지를 합해 충족될 수 있음을 의미한다.  
    a자원: 현재 사용 가능한(available) 자원, b자원: i보다 앞선 (j < i) 모든 Pj가 점유하고 있는 자원들  
    a + b를 통해 Pi의 최대 자원 요청을 만족시킬 수 있다.

**불안정 상태(unstable state)**
- 프로세스의 안정 순서가 존재하지 않는 상태
- 교착상태는 불안정 상태일 때 발생하지만, 불안정 상태라고 해서 교착상태인 것은 아니다. 

**방법**
- 시스템이 안정 상태를 유지하도록 자원 할당을 처리함으로써 교착상태를 회피한다.
- 안정 상태에서 자원을 할당해서 다른 상태로 전이하더라도 안정 상태가 되도록 유지한다.  
  즉, 자원 요청을 받아드렸을 때, 불안정 상태가 되면 요청을 거절한다.

**예시**  
프로세스 P0, P1, P2, P3와 동일한 유형의 자원 10개를 가진 시스템

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-Avoidance-state-ex1.png' width='500'>

- 안정 상태
  
    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-Avoidance-state-ex2.png' width='500'>

    - 안정 순서 <P2, P0, P1, P3>가 존재하기에 안정 상태이다.
    - 자원의 최대 개수 10개를 초과하지 않고 순서대로 프로세스 처리가 가능하다.

- 불안정 상태
  
    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-Avoidance-state-ex3.png' width='500'>

    - 안정 순서가 존재하지 않으므로, 교착상태 발생 위험이 있다.
    - 교착상태가 발생하지 않을 수도 있다.
      - P2가 자원 2개 할당 받아 실행 완료 (4) → P3이 한 개 반납 (5) → P0이 5개를 할당받아 실행 완료 (5) → P1 실행 완료 (1) → P3 실행 완료 (10)
    - 교착상태가 발생하는 경우
      - P2 실행을 마치고 반납 사용 가능 자원 수 4개 → P0이 5개를 요구하는 경우 교착상태 발생

#### 은행원 알고리즘(Banker's algorithm)
- 다익스트라 은행원 알고리즘을 이용한 교착상태 회피 방법이다.
- 각 프로세스가 자원 종류별 최대 요청 수를 파악해두고, 자원 요청이 있을 때마다 다음과 같이 결정한다.
  - 요청을 수락해도 안정 상태를 유지할 수 있다면 요청을 수락
  - 요청을 수락한 경우 불안정 상태로 변화한다면 요청을 거절

**단점**
- 프로세스 수와 자원 수가 일정해야 한다.
- 각 프로세스가 요청할 자원 유형별 최대치 정보를 미리 파악할 수 있어야 한다.
- 프로세스가 자원을 요청할 때마다 교착상태 회피 알고리즘을 수행해야 하므로 시스템 부하가 증가한다.
  - 안정, 불안정 판정 연산
- 불안정 상태를 방지해야하므로 자원 이용도가 낮다.
  - 요청하는 자원이 충분히 남아 있어도 불안정 상태가 될 수 있는 요청이면 거부하기에 자원 이용도가 낮아진다.

**구현 방법**
- 프로세스 수는 n, 자원 종류는 m(한 종류의 자원이 여러 개)일 때,
  - Allocation: 현재 각 프로세스에 할당된 자원 수를 표시하는 n x m 행렬
  - Max: 각 프로세스의 최대 자원 요구를 표시하는 n x m 행렬
  - Need: 각 프로세스의 최대 추가 자원 요구를 표시하는 n x m 행렬
  - Available: 가용 자원 수를 표시하는 길이 m인 백터

**수행 과정**

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-Avoidance-Bankers-algorithm.png' width='600'>

**예시**  
프로세스 5개(P0~P4), 자원은 3종류(A: 10, B: 5, C: 7)인 시스템
- 현재 상태

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-Avoidance-Bankers-algorithm-ex1.png' width='500'>

- 안정 상태

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-Avoidance-Bankers-algorithm-ex2.png' width='500'>
    
- 불안정 상태

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-Avoidance-Bankers-algorithm-ex3.png' width='500'>

- 전체 흐름

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-Avoidance-Bankers-algorithm-ex4.png' width='600'>

### 교착상태 탐지와 회복(DeadLock Detection and Recovery)
- 교착상태 발생을 허용하되 교착상태를 알아내고 교착상태로부터 벗어나 회복할 수 있게 한다.
- 교착상태 탐지 알고리즘 실행시 시스템에 부담이 생긴다.
- 교착상태 회복 과정에서 수행한 작업의 손실이 발생한다.

### 교착상태 탐지(Deadlock Detection)
- 교착상태 존재 여부를 알아내고, 교착상태와 연관된 프로세스와 자원을 알아낸다.
  - circular wait 존재 여부에 초점을 맞추고 circular wait을 해결함으로써 교착상태를 해결한다.

#### 교착상태 탐지 알고리즘 호출
- 탐지 알고리즘 호출 문제는 교착상태 발생 빈도수와 교착상태 발생 시 영향을 받는 프로세스 수에 따라 결정된다.
- 교착상태가 발생하면 해결될 때까지 프로세스에 할당된 자원들은 유휴상태가 되고, 교착상태에 연관된 프로세스 수가 점점 늘어남에 따라 규모가 커진다.  
   Why? 교착상태에 연관된 자원을 다른 프로세스가 요청하면 해당 프로세스도 교착상태에 연관되어 교착상태 큐모가 확장된다.
- 교착상태 탐지 알고리즘을 자주 호출하여 해결할 수 있지만 자주 호출할 수록 시스템 부하가 증가한다.
- 지나친 시스템 부하 증가를 막는 경제적인 방법은 교착상태 탐지 알고리즘 횟수를 줄이는 것이다.
  - 특정 시간 마다 호출
  - CPU 이용률이 일정 수치 이하로 떨어질 때마다 호출(이용률 ↓ = 교착상태 가능성이 높음)

#### 자원 할당 그래프 소거(reduction of resource allocation graph) 방법
- 모든 프로세스에 의해 그래프가 소거될 수 있으면 교착상태는 없다. 즉, 소거될 수 없다면 교착상태가 존재한다.
- 어떤 프로세스와 어떤 자원이 교착상태에 연관되어 있는지를 알아낼 수 있다.
- 어떤 프로세스의 자원 요청을 수락할 수 있으면 그 프로세스에 의해 그래프가 소거될 수 있다.
  - 해당 프로세스는 실행을 마치고 자원을 반납할 수 있는 프로세스이다.
  - 그래프 소거: 해당 프로세스에서 자원으로 향한 화살표와 자원에서 그 프로세스로 향한 화살표를 모두 제거
 
**자원 할당 그래프 소거 예) 시스템 전체**  

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-dection-recovery-graph-ex1.png' width='300'>

- 소거 가능한 상태
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-dection-recovery-graph-ex2.png' width='300'>

- circular wait이 존재하여 교착상태가 존재한 상태
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-dection-recovery-graph-ex3.png' width='300'>

#### 쇼사니(Shoshani)와 코프만(Coffman)의 교착상태 탐지 알고리즘
- 현재 자원의 할당 상태에 관한 정보를 관리하고, 이 상태 정보에 의해 교착상태인지 여부를 판단할 수 있는 알고리즘

**자료 구조**  
프로세스 수는 n, 자원의 종류는 m(한 종류의 자원이 여러 개) 일 때
- Allocation: 현재 각 프로세스에 할당된 자원 수를 표시하는 n x m 행렬
- Request: 각 프로세스의 현재 요청을 표시하는 n x m 행렬
- Available: 가용 자원 수를 표시하는 길이가 m인 벡터

**수행 과정**

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-dection-recovery-algorithm.png' width='500'>

- Allocation이 0이 아닌 경우 → 할당 받은 자원이 존재한다.
- Work = Work + Allocation → 작업을 마친 경우를 의미한다.

**예시**
- 교착상태가 아닌 예)

    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-dection-recovery-algorithm-ex1.png' width='500'>
    
     - <P0, P2, P3, P1, P4> 순서로 모든 프로세스의 작업을 완료할 수 있다.
     
- 교착상태의 예)

    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/DeadLock-dection-recovery-algorithm-ex2.png' width='500'>

     - P0이 완료하고 점유한 자원을 반납하더라도 <P1, P2, P3, P4>가 연관된 교착상태가 존재한다.

### 교착상태 회복(Deadlock Recovery)
- 교착상태에서 회복한다는 것은 순환대기(circular wait) 상태에서 벗어난다는 것을 의미한다.
- 교착상태 회복은 특정 프로세스를 강제로 제거하거나 자원 반납을 요구하므로 보통 수행한 작업을 잃어버린다.

#### 프로세스 중지
- 교착상태의 프로세스들 중 하나 이상을 중지시키는 방법으로 중지된 프로세스에 할당된 모든 자원 해제를 요구한다.
- 교착상태의 모든 프로세스를 중단시키는 방법과 한 프로세스씩 부분 종료시키는 방법이 있다.

**교착상태 프로세스를 모두 중지**
- 교착상태의 순환대기를 확실하게 해결하지만 자원 사용과 시간 면에서 큰 비용이 들어간다.

**한 프로세스씩 중지(부분 중지)**
- 상대적으로 비용이 낮다.
- 한 프로세스가 중지될 때마다 교착상태 탐지 알고리즘을 호출하여 프로세스가 교착상태에 있는지 확인한다.
- 교착상태 탐지 알고리즘 호출 부담이 크다.
- 어느 프로세스를 중지할 지를 결정해야 한다.

**중지 프로세스 선정 기준**
- 프로세스 우선순위
  - 낮은 우선순위를 먼저 중지시킨다.
- 프로세스가 수행된 시간과 아픔으로 종료하는 데 필요한 시간
  - 수행된 시간이 적고 앞으로 수행할 시간이 긴 경우 중지
- 프로세스가 사용한 자원 형태와 수
  - 중단 가능한 자원인지에 대한 여부를 판단하여 중단 가능한 경우 중지
- 프로세스 종료를 위해 필요한 자원 수
  - 종료를 위해 필요한 자원 수가 적은 경우 종료
- 중지해야할 프로세스의 수
  - 중지할 프로세스 수가 적은 경우 종료
- 프로세스가 대화식인지 일괄식인지 여부
  - 한번에 모아서 처리하는 일괄식인 경우 종료

#### 자원 선점
- 교착상태가 해결 될 때까지 프로세스의 자원을 빼앗아 다른 프로세스에게 할당한다.
  - 중지시키지 않고 자원만을 빼앗아 할당한다.

**해결 과제**
- 선점 자원 선택
  - 비용 최소화를 위해 적절한 선점 순서를 결정해야 한다.
- 복귀
  - 자원을 빼앗긴 프로세스는 정상적으로 실행할 수 없으므로 프로세스를 안전한 상태로 복귀시키고 다시 시작해야한다.
  - 작업 중지 시 프로세스가 작업한 결과를 잃어버리게 된다.
- 기아
  - 비용에 근거한 시스템에서는 동일한 프로세스가 반복하여 희생자로 선택되기 쉽다.
  - 프로세스가 짧은 시간 동안만 희생자로 선택됨을 보장해야한다.
  - 일반적인 해결 방법으로는 비용 요소에 복귀 횟수를 포함시큰 것이다.  
    복귀 횟수 증가 → 비용 증가 → 기아상태 발생 억제

## 요약
- 프로세스가 결코 일어나지 않을 사건을 기다리는 상태를 교착상태(DeadLock)라고 한다.
- 교착상태는 상호배제(mutual exclusion), 점유와 대기(hold and wait), 비선점(no-preemption), 순환대기(circular wait) 조건을 모두 만족할 때 발생한다.
- 시스템의 자원 할당과 요청 관계를 표현한 방향 그래프인 자원 할당 그래프에 사이클이 있는 경우 교착상태가 발생할 수 있으며 발생하지 않을 수도 있다.
- 교착상태 문제를 해결하기 위해 예방, 회피, 탐지와 회복 방법을 사용할 수 있다.
- 교착상태 예방(deadlock prevention)
  - 교착상태가 절대 일어나지 않도록 방지한다.
  - 명쾌하지만 자원 활용도가 떨어진다.
- 교착상태 회피(deadlock avoidance)
  - 시스템 내 교착상태 가능성은 있지만 교착상태를 회피하여 절대 교착상태가 일어나지 않는다.
  - 회피 알고리즘 실행으로 시스템 부하가 증가한다.
  - 자원 요청시 마다 회피 알고리즘을 실행하기에 교착상태 해결 방법 중 가장 시스템 부하가 심하다. 
- 교착상태 탐지와 회복(deadlock detection and recovery)
  - 교착상태 발생을 허용하되 교착상태를 알아내고, 교착상태로부터 벗어나 회복할 수 있게 한다.
  - 교착상태 탐지 알고리즘 실행시 시스템에 부하가 증가한다.
  - 교착상태 회복 과정에서 수행한 작업의 손실이 있다.
- 위의 세 가지 방법 외에 시스템에서 교착상태를 무시하는 방법도 있다.
  - 이 경우 교착상태 발생시 시스템 재시작 등의 방법으로 해결한다.
- 한 가지 방법으로만 시스템의 모든 자원 할당 문제를 해결하는 것은 불가능하다.
  - 세 가지 방법을 결합하여 자원의 형태에 따라 최적의 접근 방법을 채택하여 해결한다. 


> ⬆️:[Top](#교착상태DeadLock)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Operating-System)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [구현회. 운영체제-그림으로 배우는 구조와 원리, 개정3판. 한빛아카데미]
