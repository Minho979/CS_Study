# 상호 배제(Mutex: Mutual Exclusion)
## 생산자-소비자 문제
- 비동기적 프로세스들이 작업 수행을 위해 서로 협동하고, 병행 수행하는 대표적인 예시이다.
- 생산자 프로세스는 소비자 프로세스가 소비하는 정보를 생산한다.
- 상호배제와 동기화를 필요로 한다.

### 생산자-소비자의 공유 버퍼(공유 자원)
- 생산자의 데이터 생산과 소비자의 데이터 소비는 서로 독립적이므로 공유 버퍼를 필요로 한다.
- 생산자와 소비자는 같은 버퍼를 사용하므로 공유 변수에 동시에 접근하는 경우 문제가 발생할 수 있다.
  - 생산자가 이미 채워진 버퍼에 더 채우거나 소비자가 빈 데이터를 꺼낼 때 문제가 발생한다.

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-Producer-Consumer-buffer.png' width='500'>

#### 유한 버퍼의 구현
- 2개의 논리적 포인터 in과 out을 갖는 queue 순환 배열로 구현한다.
- 순차 리스트 버퍼의 경우 삽입, 삭제시 인덱스와 데이터가 이동하는 오버헤드가 발생하여 비효율적이다.

### 공유 변수 동시 접근 문제
- 공유 변수 조작 부분에 동시에 접근할 시 문제가 발생한다.
#### 공유 변수 동시 접근
- 생산자 프로세스와 소비자 프로세스가 counter 변수에 동시 접근 시 counter에 잘못된 값이 저장될 수 있다.
- 예) counter가 5인 경우

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-Producer-Consumer-ex.png' width='500'>

### 경쟁 상태(Race Condition)
- 여러 프로세스가 동시에 공유 데이터에 접근할 때, 접근 순서에 따라 실행 결과가 달라지는 상황을 말한다. 
- 해당 상황을 방지하기 위해서는 병행 프로세스들을 동기화해야 한다.
  - 세마포어(Semaphore)
  - 상호 배제(Mutex)
  - 모니터(Monitor)

## 임계 영역(Cirical Section)
- 다수의 프로세스가 실행 가능한 영역이면서 한 순간에 하나의 프로세스만 실행할 수 있는 영역이다.
- 공유 자원의 독점을 보장하기 위한 코드 영역이다.
- 프로세스가 공유 데이터(임계 자원)에 접근하는 동안 그 프로세스는 임계 영역에 있다고 표현한다.
- 4가지 코드 영역으로 구성되어 있다.
  - 진입 영역(entry section): 임계 영역에 들어갈 수 있는지 알아보고 허락 받는 코드 부분
  - 임계 영역(critical section): 한 순간에 한 프로세스만 실행해야하는 코드 부분
  - 탈출 영역(exit section): 임계 영역 수행을 마치고 나갈 때 필요한 작업을 수행하는 코드 부분
  - 나머지 영역(remainder section): 임계 영역과 관계 없는 나머지 코드 부분

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-Cirical-Section1.png' width='600'>

### 임계 영역 문제 해결 조건 
1. 상호 배제(Mutex)
   - 한 프로세스가 임계 영역에 있는 경우 다른 프로세스는 진입이 불가능해야 한다.
2. 진행(Progress):
   - 임계 영역에 진입한 프로세스가 없는 상태에서 임계 영역에 진입하려는 여러 프로세스가 있는 경우 선택하여 진입하게 해야한다.
3. 유한 대기(Bounded Waiting)
   - 다른 프로세스의 기아를 방지하기 위해, 임계 영역에 한 번 진입했던 프로세스에게 진입 요청 허가의 제한을 두어 무한정 대기 상태를 막는다.
  
### 임계 영역 문제 해결책의 가정 
- 각 기계어 명령어는 분할할 수 없게 실행한다.
  - 하나의 기계어 명령어를 시작하면 인터럽트의 영향을 받지 않고 해당 명령어를 끝까지 실행한다.
- 각 프로세스가 nonzero speed로 실행한다고 가정한다.
  - nonzero speed: 프로세스가 명령어를 실행하는 도중 멈추는 일이 없다. 
- 프로세스들의 상대적인 속도에 대해서 어떠한 가정을 하지 않는다.

### 임계 영역 문제 해결 방법
- 임계 영역 내 인터럽트를 방지한다.
  - 단일 프로세서 환경에서만 사용할 수 있다.
- 임계 영역에 대한 프로세스 동기화를 진행한다.
  - 한 프로세스가 임계 영역 내에 있을 때 다른 프로세스들은 임계 영역에 진입이 금지된다.
  - 세마포어(Semaphore), 상호배제(Mutex), 모니터(Monitor)가 있다.

#### 임계 영역 프로세스 동기화 

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-Cirical-Section2.png' width='600'>

## 상호 배제(Mutex)
- 한 순간에 하나의 프로세스만을 사용할 수 있는 공유자원에 대해, 한 프로세스가 공유 자원을 사용하는 동안 다른 프로세스가 그 자원에 접근할 수 없게 차단하는 것을 말한다.
- 상호 배제를 위해서는 프로세스 동기화(synchronization) 또는 락(Lock) 이 필요하다.
  - 순차적으로 재사용이 가능한 자원을 공유하는 프로세스들이 공유자원을 동시에 사용하지 못하게 실행 제어하기 위해 프로세스 동기화가 필요하다. (쓰기 연산)
  - 순차적 재사용은 자원을 한 프로세스가 사용한 다음 이어서 다른 프로세스가 사용이 가능하다.
  - 락(Lock): 자원에 대한 접근 제한을 가젱하기 위한 동기화 매커니즘으로 임계 영역에 진입 시 프로세스는 락을 걸고(취득 불가 상태로 전환), 해당 프로세스는 임계 영역을 벗어날 때 락을 반환(취득 가능 상태로 전환)한다.
- 읽기 연산은 상호배제가 필요하지 않다.
  - 프로세스들이 충돌이 없는 연산을 수행하는 경우 공유 자원에 동시에 접근할 수 있다.
- Key(어떤 객체)를 기반으로 상호배제를 진행한다.

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion.png' width='600'>

### 상호 배제의 조건
1. 두 개 이상의 프로세스들이 동시에 임계 영역(공유 자원)에 있으면 안된다.
2. 어떤 프로세스도 임계 영역(공유 자원)에 진입하는 것이 무한정 연기되면 안된다.
3. 임계 영역(공유 자원) 안에 있는 프로세스가 다른 프로세스의 임계 영역 진입을 막을 수 있어야 한다.
4. 프로세스들의 상대적인 속도(각 프로세스들의 처리 속도, 접근 방법, 상태)에 대해 어떠한 가정을 하면 안된다.

## 상호 배제 방법
상호 배제, 세마포어, 모니터, 하드웨어 명령어 방법으로 상호 배제와 임계 영역, 동기화 문제를 해결할 수 있다. 
### 상호 배제(Mutex)
- 소프트웨어적인 임계영역 문제 해결이라고도 불린다.
- 특별한 하드웨어 명령어를 필요로 하지 않는 해결책이다.
  - entry, exit code 작성
- 공유 자원이나 임계 영역에 접근하려면 Key를 가진 프로세스나 스레드만 가능하다.
- 바쁜 대기(busy-waiting)로 프로세서 시간이 낭비된다.
  - 바쁜 대기(busy waiting): 어떤 조건을기다리는 프로세스들이 비생산적으로 자원을 소비하는 대기 루프에 있는 상태
- 데커 알고리즘, 피터슨 알고리즘, 햄포트의 베이커리 알고리즘, 크누스 알고리즘, 핸슨 알고리즘, 다익스트라 알고리즘 등이 있다.

#### 데커(Dekker) 알고리즘
- 두 프로세스의 임계영역 문제를 하드웨어 도움 없이 순순하게 소프트웨어적으로 해결하는 방법이다.
- 임계영역 문제 해결책의 조건을 만족한다.
- 구현
  - 프로세스가 P0, P1일 때 공유변수 `flag`, `turn`을 가진다.
  - `flag[0]`: P0가 임계 영역 진입 `flag[1]`: P1이 임계 영역 진입
  - `turn`: 정수형 변수로 값이 0인 경우 P0에게 진입 우선권, 1인 경우 P1에게 진입 우선권을 부여한다.

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-Dekker1.png' width='600'>
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-Dekker2.png' width='600'>

#### 피터슨(peterson) 알고리즘
- 데커 알고리즘과 비슷하지만 상대적으로 피터슨 알고리즘이 간단하다.
- turn에 동시 접근 문제가 발생하지 않는다.
- 순차적으로 실행된다. 

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-Peterson.png' width='600'>

### 하드웨어 명령어
- 특수한 하드웨어 명령어를 제공하는 경우, 순수한 소프트웨어적인 방법보다 임계 영역 문제를 해결하는 알고리즘이 간단해진다.
- 임계 영역 문제를 해결에 사용할 수 있는 하드웨어 명령어는 2가지이다.
  - TestAndSet: 내용을 검사 및 수정하는 명령어
  - Swap: 두 내용을 서로 바꾸는 명령어
- 하드웨어 명령어를 제공하지 않는 시스템에서는 사용할 수 없다.

#### TestAndSet(TAS)
- 수행하는 작업이 복잡하다.
- 다음과 같은 원자적 연산(atomic operation)을 수행한다.
  - 원자적 연산: 중간에 인터럽트가 발생하지 않고 단번에 수행하는 최소 단위의 기계어 명령어

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-TAS1.png' width='500'>

- 프로세스가 2개인 경우 TAS
``` java
while(true) {
	while (TestAndSet(&lock)); // lock을 검사하여 ture면 대기(entry)
	// false이면 true로 변경, true이면 false가 될 때까지 기다림 
	/*임계영역*/;
	lock - false; // 다른 프로세스 진입 허용(exit)
	/* 나머지 영역*/;
}
```
-
  - 단일 프로세서 뿐 아니라 메모리를 공유하는 다중 처리 환경에도 적용이 가능하다.
  - 임계 영역에 진입하는 프로세스에 바쁜 대기가 발생한다.
  - 프로세스가 2개 초과인 경우 일부는 무기한 연기에 빠질 수 있다.

- 여러 프로세스의 TAS

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-TAS2.png' width='600'>

### 세마포어(Semaphore)
- 공유 자원의 데이터 혹은 임계 영역에 설정한 수 만큼의 프로세스나 스레드만 접근하도록 막아준다.
- 동시에 접근할 수 있는 프로세스나 스레드의 수를 세마포어 변수를 통해 관리하며 상호 배제를 보장한다.
- 세마포어의 초기화 이후에는 두 가지 연산(P, V)으로만 접근할 수 있는 보호 정수 변수이다.
- P, V 연산이 프로그램 전체에 퍼져있으며 이 연산이 미치는 영향을 전체적으로 파악하기 어려워 프로그램 작성이 어렵다.

- 세마포어의 예) 열차의 차단기

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-semaphore-ex.png' width='400'>

  - 차단기가 올라간 상태: 정지/대기 (자원이 없어 기다려야하는 경우)
  - 차단기가 내려간 상태: 진행(프로세스가 해당 자원을 이용할 수 있는 자유 상태)

#### 세마포어 사용시 유의사항
- P 또는 V 연산을 빠뜨리거나 잘못 허용하는 경우
  - 상호배제나 동기화가 제대로 이루어지지 않을 수 있다.
  - P 연산 과정에서 대기하고 있는 프로세스들이 교착 상태에 빠질 수 있다.
    - 교착 상태: 대기 상태에서 영원히 빠져나오지 못하는 상태

#### 세마포어의 연산
- 초기화
- **P 연산**
  - 프로세스를 대기시키는 wait 동작
  - 임계 영역 문제에서는 진입 코드(entry section)로 사용한다.
- **V 연산**
  - 대기 중인 프로세스를 깨우는 신호를 보내는 signal 동작
  - 대기중인 프로세스에 들어갈 수 있다는 신호를 보낸다.
  - 임계 영역 문제에서는 탈출 코드(exit section)로 사용한다.

- 프로세스 하나가 세마포어(S)의 값을 수정할 때 다른 프로세스가 동시에 수정할 수 없어야 한다.
  - P연산에서 S값 검사와 수정은 인터럽트 없이 단일 동작으로 수행되어야 한다.
  - V연산 또한 단일 동작으로 수행되어야 한다.
- P와 V의 동작은 프로세스가 시스템을 호출함으로써 운영체제에 의해 실행된다.
- P연산을 요구한 프로세스는 수행 가능한 상태(S > 0)가 될 때까지 기다려야 한다.

#### 세마포어의 사용: 임계 영역 문제 해결
- 2개 이상의 프로세스에 대해 임계 영역 문제 해결하는데 있어 세마포어를 이용할 수 있다.
  - n개의 프로세스가 1로 초기화된 세마포어를 공유한다. 
- 진입 프로세스는 공유 변수가 1일 때만 임계 영역에 진입할 수 있다.
  - 진입 프로세스는 중복 진입을 막기 위해 공유 변수를 0으로 변경하여 진입을 막고 나올 떄 1로 변경하여 진입 허용 
- 각 프로세스 Pi의 구조 (i = 0, 1, 2, ..., n-1)

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-semaphore-pi.png' width='300'>

  - P0가 P1보다 먼저 실행하는 경우 (mutex는 변수 이름)
      1. P0에서 먼저 wait 실행 (현재 mutex = 1)
      2. mutex를 0으로 감소시키고 wait 종료 후 임계 영역 진입(현재 mutex = 0)
      3. P0 임계 영역 중 P1이 wait 실행 (현재 mutex = 0)
      4. P1은 mutex 값이 0보다 커질 때 까지 기다림 (현재 mutex = 0)
      5. P0이 임계영역을 마치고 signal 실행 → mutex + 1 (현재 mutex = 1)
      6. P1이 mutex 값을 0으로 감소시키고 임계 영역 진입 (현재 mutex = 0)

#### 세마포어의 사용: 프로세스 동기화(synchronization)
- 여러가지 동기화 문제를 해결하는데 있어 세마포어를 이용할 수 있다.
- 비동기적으로 실행하지만 어떤 문장에 대해 실행 순서를 지켜야하는 경우 사용한다.
- 예) 두 개의 프로세스 S0이 끝난 후 S1 수행

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-semaphore-synch.png' width='500'>
  
  - P0과 P1이 세마포어 synch를 0으로 초기화 후 공유
    - synch: 기다리는 사건(S0의 실행)이 발생했는지를 나타냄
  - P0에는 signal, P1에는 wait을 통해 synch가 1이 되는 경우 P1 실행

#### 세마포어의 종류
- 이진 세마포어(binary semaphore)
  - 0과 1 값만 가지는 세마포어
  - 예) 상호 배제 문제 해결을 위해 공유변수 1로 초기화
- 계수 세마포어(counting semaphore)
  - 정수 값을 가지는 세마포어
  - 예) 유한한 자원에 접근하는 것을 제어하기 위해 사용 가능한 자원 수로 초기화  
    n개의 유한 자원 → n으로 초기화

#### 세마포어의 구현
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-semaphore-busy-waiting.png' width='300'>

일반적으로 wait 연산에서 바쁜 대기 문제가 발생할 수 있지만 아래의 방법을 통해 예방이 가능하다.

  - 프로세스들이 동시에 P, V 연산을 수행할 수 없어야 한다.
    - 단일 프로세서의 경우 P, V 연산 중 인터럽트 금지를 통해 해결 가능
    - 다중 프로세스의 경우 인터럽트로 해결이 불가능하며, 하드웨어 명령어를 지원하지 않는다면 소프트웨어적으로 해결해야한다.  
      이떄, P 프로시저와 V 프로시저는 임계 영역이 된다.
  - 세마포어는 대기 리스트를 가지는 정수 변수 구조로 정의한다. 

    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-semaphore-structure.png' width='350'>

#### 동작
  1. 세마포어 대기 리스트를 만들어 세마포어 값이 양수가 아닌 경우 대기하도록 한다.
      - 해당 대기는 대기 리스트의 대기로 바쁜 대기 상태가 아니다.
  2. 이후 프로세스 스케줄러는 준비 큐에서 다른 프로세스를 선택하여 수행한다.
  3. 세마포어 대기 리스트에서 대기중인 프로세서는 V 연산이 실행될 때까지 대기한다.
  4. 대기 상태에서 빠져나온 프로세스는 준비 큐에 들어간다. (바로 재실행되지는 않음)

- 바쁜 대기 문제를 해결한 counting semaphore 동작 정의)

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-semaphore.png' width='500'>

### 모니터(Monitor)
- 동기화를 자동으로 제공하는 병행 프로그래밍 구조를 말한다.
- 공유 데이터, 하나 이상의 프로시저, 초기화 코드로 구성된 객체이다.
- 모니터 밖에 있는 프로세스는 모니터의 데이터에 접근이 불가능하다.
  - 모니터 외부에서는 공유 데이터 접근이 불가능하기에 모니터 진입 루틴을 통해 원하는 작업을 요청한다.
- 모니터 경계에서 한 번에 프로세스만 진입하도록 제어하기에 상호 배제 원칙이 자동으로 지켜진다.
  - 한 프로세스가 모니터 진입 루틴을 호출하여 실행중인 경우 진입을 원하는 다른 프로세스는 모니터 밖 진입 큐에서 대기한다.
  - 프로그래머가 직접 동기화 제약 조건을 명시적으로 코드화할 필요가 없다. 

#### 모니터 구성
- 공유 데이터: 프로시저들이 공유하는 변수
- 모니터 진입 루틴: 모니터의 서비스를 이용하기 위해 외부에서 호출할 수 있는 프로시저
- 초기화 코드

#### 모니터의 구조 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-Moniter-structure.png' width='600'>

#### 모니터의 조건 변수
모니터 루틴 수행 중에 프로세스가 대기하는 경우, 대기 조건을 나타내기 위해 조건 변수를 가질 수 있다.
- 하나 이상의 조건 변수를 정의할 수 있다.
- 조건 변수에는 wait과 signal 연산만 수행이 가능하다.
  - 조건 변수 x의 연산
  - x.wait: 조건 변수 x의 큐에서 대기하기에 모니터 진입 큐에서 대기하거나 바쁜 대기 상태가 아니다. 
    - x.wait을 실행한 프로세스는 다른 프로세스가 x.signal을 수행할 때까지 x의 큐에서 대기한다.
  - x.signal
    - x.wait을 실행하여 x의 큐에서 대기중인 프로세스들 중 하나를 꺼내 모니터로 진입할 수 있도록 한다.
    - x의 큐에 신호를 보내 대기중인 프로세스가 있다면 꺼내어 모니터의 엔트리 큐에 집입할 수 있게한다.
    - x의 큐에 대기중인 프로세스가 없다면 해당 연산을 수행해도 아무런 변화가 없다.
- 모니터 진입 큐와는 별도로 각 조건 변수마다 하나의 큐를 가진다.

- 조건 변수를 갖는 모니터의 구조

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-Moniter-structure2.png' width='600'>

#### 모니터의 사용: 임계 영역 문제 해결
- 모니터 진입 루틴 프로시저를 통해 자동으로 상호 배제를 진행하기에 모니터의 프로시저는 임계 영역이 된다.

#### 모니터의 사용: 자원 할당
1. 자원 할당을 담당하는 하나의 모니터 객체를 생성한다.
2. 자원을 요청한 프로세스는 요청을 위한 모니터 진입 루틴을 호출한다.
    - 자원을 할당 받은 경우: 프로시저 수행을 마치고 모니터를 떠나기 위해 반납을 위한 루틴 수행한다.
    - 자원을 할당 못받은 경우: 대기한다.
3. 자원 반납 프로세스는 반납을 위한 모니터 진입 루틴을 호출한다.
    - 호출된 루틴은 대기 중인 프로세스에 신호를 보내고, 모니터는 대기 중인 프로세스에게 자원을 할당한다.

- 단일 자원 할당 모니터 예)

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-Moniter3.png' width='500'> 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-Moniter1.png' width='500'>
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Mutual-Exclusion-Moniter2.png' width='500'>

## 요약 
- 경쟁 상태(race condition)는 동시에 공유 데이터에 접근할 때 프로세스의 접근 순서에 따라 실행 결과가 달라지는 상황을 말한다.
- 경쟁 상태를 방지하기 위해 프로세스 실행을 동기화해야 한다.
- 상호 배제(mutual exclusion)는 한 프로세스가 공유 자원을 사용할 때 다른 프로세스가 접근하지 못하게 하는 것이다.
- 임계 영역(critical section)은 한 순간에 한 프로세스만 실행할 수 있는 영역이다.
- 임계 영역을 사용하여 상호 배제를 구현할 수 있다.
- 데커의 알고리즘, 베이커리 알고리즘 등 소프트웨어적으로 구현한 상호배제를 통해 임계영역 문제를 해결할 수 있다.
- 하드웨어 명령어인 TestAndSet를 이용하면 소프트웨어적인 방법보다 조금 더 간단한 방법으로 임계영역 문제를 해결할 수 있다.
- 세마포어(semaphore)를 이용하여 임계영역 문제를 포함한 보다 다양한 동기화 문제를 해결할 수 있다.
- 세마포어(semaphore)는 P, V 연산을 프로그래머가 적절한 위치에 삽입해야하는 한계를 가진다.
- 세마포어를 잘못 사용하면 여러 오류가 쉽게 발생한다. 모니터(monitor)는 이 단점을 극복하기 위한 병행 프로그래밍 구조이다.
- 모니터는 모니터의 경계에서 상호배제를 자동으로 구현하며 조건 변수를 가질 수 있다.


> ⬆️:[Top](#상호-배제Mutex-Mutual-Exclusion)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Operating-System)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [구현회. 운영체제-그림으로 배우는 구조와 원리, 개정3판. 한빛아카데미]
