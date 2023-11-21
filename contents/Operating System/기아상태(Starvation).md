# 기아상태(Starvation)
- 프로세스가 작업을 수행하지 못하고 무기한 기다리는 상태
- 교착상태는 아니며 자원 할당이 무기한 연기(indefinite postponement)되는 상태
- 프로세스의 우선순위에 따라 자원을 할당하는 경우, 우선순위가 낮은 프로세스는 기아상태가 될 수 있다.
  - 에이징(aging): 어떤 자원을 오래 대기할 수록 프로세스의 우선순위를 높여준다.

## 식사하는 철학자 문제 
병행 프로세스의 교착상태와 기아상태를 설명하는 고저적인 프로세스 동기화 문제
- 5명의 철학자는 생각하고 식사하는 일을 반복한다.
- 테이블에는 중앙에 음식이 있으며, 포크 5개가 철학자 사이에 하나씩 놓여 있다.
- 철학자는 좌우 철학자와 포크를 공유하되, 하나의 포크를 둘이 동시에 사용할 수는 없다.
- 식사할 떄는 각자의 좌우 포크를 2개를 사용하고, 식사를 마치면 포크를 내려놓은 뒤 생각한다.

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Starvation.png' width='500'>

### 세마포어를 이용한 문제 해결 방법
- **포크를 세마포어로 표시하여 상호배제를 구현한다**
  - 포크를 양쪽 철학자가 동시에 사용할 수 없으므로 각 포크에 대한 상호배제가 필요하다.
  - 포크를 집으려면 P연산을 수행, 내려놓으려면 V연산을 수행
  - 교착상태가 발생할 수 있다.
    - 5명의 철학자들이 동시에 모두 왼쪽 포크를 먼저 집어들고, 오른쪽 포크를 집으려하는 경우 교착상태가 발생한다.

    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Starvation_deadlock.png' width='250'>

#### 구조
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Starvation1.png' width='500'>

#### 교착상태 예방을 위한 해결책
- **철학자 4명만 테이블에 동시에 앉도록 하는 방법**
  - 적어도 1명은 식사가 가능하며 나미지 철학자들도 1명 식사후 식사가 가능하다.

    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Starvation2.png' width='500'>

- **철학자가 양쪽 포크 모두 사용 가능할 때만 포크를 집을 수 있도록 허용하는 방법**
  - 양쪽 포크를 한번에 집도록 하며 해당 작업을 임계 영역에서 수행한다.
  - 할당을 받기 위해서는 필요로 하는 자원을 사용중인 프로세스가 사용을 마쳐야 요청 후 할당받을 수 있다.

- **비대칭 해결법을 사용하는 방법**
  - 홀수번째의 철학자는 왼쪽 포크를 집은 후 오른쪽 포크를 집으며 짝수번째는 이와 반대로 수행한다.
    - 0은 짝수로 여긴다.
  - 사이클의 생성을 막아 교착상태를 예방한다.
  - 자원을 할당받지 못한 프로세스는 추가적인 자원할당 요청을 할 수 없다.
  - 만약 필요로 하는 자원을 하나라도 사용 중인 프로세스가 있다면 할당 요청도 불가능하다.
 
  - 예시
    
    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Starvation.png' width='350'>

    - 철학자 0은 fork1 요청 후 fork0을 요청할 수 있다.
    - 철학자 1은 fork1 요청 후 fork2를 요청할 수 있다.

#### 해결책의 한계
- 교착상태 해결책은 기아상태의 가능성을 제거하지 못한다.
  - 기아상태를 방지해야 한다.
  - 기아상태를 해결하기 위해 먼저 기다리는 작업을 발견하고 각 작업이 기다린 시간을 조사, 추적해야한다.
  - 기아상태를 발견하는 즉시 새로운 작업의 시작을 대기하도록 시스템이 조치해야 한다.
  - 빈번한 시스템 대기로 처리량이 감소할 수 있다.

> ⬆️:[Top](#기아상태Starvation)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Operating-System)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [구현회. 운영체제-그림으로 배우는 구조와 원리, 개정3판. 한빛아카데미]
