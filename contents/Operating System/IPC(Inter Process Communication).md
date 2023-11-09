# IPC(Inter Process Communication)
## 개념
프로세스들 간에 서로 데이터를 주고 받는 행위 또는 그에 대한 방법이나 경로를 말한다.

프로세스(Process)는 독립적으로 실행되는 객체이며 주소 공간이 분리되어 있어 다른 프로세스의 공간에 액세스할 수 없다. 하지만 프로세스는 정보 공유, 계산 속도 향상, 모듈성, 편의성 등을 위해 통신을 필요로 할 수 있다. 
이를 위해 운영체제는 독립적인 프로세스 간 데이터를 교환할 수 있는 프로세스 간 통신 IPC를 제공한다. 

## IPC 라이브러리 
- System V의 IPC 라이브러리
  - 공유 메모리에 접근하기 위한 공유키에 16비트 정수를 사용한다.
- POSIX 표준 IPC 라이브러리
  - 공유 메모리에 접근하기 위한 공유키에 파일 경로명을 사용한다.

2가지로 나뉘며 사용 방법에 있어서 큰 차이점을 보이지 않는다. 

## IPC 모델
IPC의 기본 모델은 공유 메모리 모델(Shared-memory Model)과 메시지 패싱 모델(Message-passing Model) 두 가지로 나뉜다. 
- 공유 메모리 모델(Shared-memory Model): Shared Memory, Memory Map, Semaphore
- 메시지 패싱 모델(Message-passing Model): Signal, PIPE, FIFO, Message Queue, Socket, Semaphore

## 공유 메모리 모델(Shared-memory Model)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/IPC-Shard-Memory-Model.png' width='300'>

- 프로세스 간 공유 메모리 영역을 설정하고 공유 영역에서 데이터를 읽고 쓰는 방식으로 데이터를 교환한다.
- 프로세스 간 read, write 연산이 모두 필요할 때 사용한다. 
- 시스템 호출이 메모리 생성 및 제거할 때에만 필요하기 때문에 커널이 개입이 적어, 메세지 패싱 모델보다 빠르다.
- 프로그램 레벨에서 통신 기능을 제공하여 자유로운 통신이 가능하다.
- 공유 메모리로 인한 동기화 문제가 발생할 수 있다.
- 동시에 같은 메모리 위치에 접근하는 위치가 발생할 수 있다.
  - 세마포어(Semaphore), locking과 같이 접근 제어 방법이 필요하다.


### 공유 메모리(Shared Memory)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/IPC-Shard-Memory2.png' width='500'>
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/IPC-Shard-Memory.png' width='600'>

- 한 시스템 내에 있는 프로세스들에 한에서만 공유되며 프로세스 중 하나가 공유 메모리를 생성하면 다른 프로세스들은 해당 공유 메모리를 읽거나 쓸 수 있다.
- 공유 메모리가 각 프로세스에게 첨부(attach)하는 방식으로 작동하게 된다.
- 대량의 정보를 다수의 프로세스에게 배포 가능하다.
- 중개자 없이 곧바로 메모리에 접근할 수 있기에 모든 IPC 중에서 가장 빠르게 작동할 수 있다. 

### 메모리 맵(Memory Map)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/IPC-Memory-Map.png' width='650'>

- 공유 메모리처럼 메모리를 공유하지만 열린 파일을 메모리에 매핑 시켜서 공유하는 방식이다.
  - 공유 매개체: 파일 + 메모리
- 주로 파일로 대용량 데이터를 공유해야 할 때 사용한다.
- FILE IO가 느릴 때 사용한다.
- 대부분 프로세스를 실행할 때 실행 파일의 각 세그먼트 메모리에 사상하기 위해 메모리 맵 파일을 이용한다.
- 메모리 맵 파일은 파일의 크기를 바꿀 수는 없으며 메모리 맵 파일을 사용하기 이전, 또는 이후에만 파일의 크기를 바꿀 수 있다. 

## 메시지 패싱 모델(Message-passing Model)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/IPC-Message-passing-Model.png' width='300'>

- 프로세스 간 공유되는 주소 공간 없이, 협력 프로세스 간 교환되는 메시지를 통해 정보를 교환한다.
- send, resive 연산을 통해 통신한다.
- 큐를 사용하여 프로세스 간 메세지를 주고 받게되며, 일반적으로 커널의 시스템 콜을 사용하여 구현된다.
- 커널의 개입으로 동기화 문제로부터 안전하다는 장점이 있다.
- 커널이 개입하므로 비교적 많은 시간이 소요된다는 단점이 있다.

### 시그널(Signal)
사용자 레벨의 인터럽트로 프로세스들끼리 혹은 커널이 프로세스에게 사건 발생을 비동기적으로 알리는 방법으로 신호 핸들러를 등록하고, 신호를 보낼 때 시스템 호출 함수를 이용한다. 
- 신호 핸들러: 사용자 공간에 작성되는 코드이며, 신호가 전달되는 과정은 커널에 의해 이루어진다.
- 신호 핸들러가 등록되어 있지 않은 경우 4가지 기본 행동 중 하나를 취한다.

  - 종료: 신호를 수신할 프로세스를 강제 종료
  - 코어 덤프: 신호를 수신할 프로세스를 강제 종료시키고 코어 파일을 생성
    - 코어 파일: 프로그램이 비정상적으로 종료될 때 프로그램의 상태 및 실행 정보를 저장하여 생성되는 파일
  - 중지: 신호를 수신할 프로세스의 실행을 일시 중지. 중지된 프로세스는 이후 계속 실행 가능
  - 무시: 신호를 무시하고 아무 처리도 하지 않음

#### 신호를 수신하게 되는 경우
- 프로세스 자신이 보낸 신호 수신
- 다른 프로세스로부터 신호 수신
- 커널로부터 신호 수신
  - ex) n으로 나누기, 자식 프로세스 종료, 시스템 알람 등의 사건

#### 신호 처리 과정
- 신호 등록: 시스템 호출을 이용하여 신호를 수신했을 때 실행시킬 핸들러를 등록한다.
- 신호 발생: 송신 프로세스가 수신 프로세스로 신호를 보낸다.
- 신호 전파: 커널이 수신 프로세스가 신호 핸들러를 실행하도록 한다.

### 파이프(PIPE)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/IPC-PIPE.jpg' width='500'>

- 익명 파이프 (Anonymous PIPE)라고도 불린다.
- 파이프(PIPE)는 두 개의 프로세스를 연결하며, 하나의 프로세스는 쓰기만 가능하고 다른 프로세스는 읽기만 가능한 형태이다.
- 해당 특성으로 인해 특성으로 반이중(Half-Duplex)통신이라고 부른다.
- 통신할 프로세스를 명확하게 알 수 있는 경우에 사용한다.
  - 외부 프로세스는 사용이 불가능하며 부모 - 자식 또는 형제 프로세스 간에 사용한다. 
- 만일 두 프로세스가 모두 읽기와 쓰기가 가능하도록 하고싶다면 송/수신 파이프를 두 개 만들어 사용해야하지만 이는 구현이 복잡하다.
- 전이중 통신이 필요한 상황에서는 낭비가 심하므로 부적합하다.
- 용량 제한이 있어 파이프가 가득차면 더 이상 사용할 수 없다. 

### Named PIPE(FIFO)
- 전혀 모르는 상태의 프로세스들 사이의 통신에 사용한다.
- 파이프의 확장이 이루어진 상태로 부모 프로세스와 무관한 전혀 다른 모든 프로세스들 사이에서도 통신이 가능하다.
  - 프로세스의 통신을 위해 이름이 있는 파일을 사용하기 때문에 다른 프로세스들과 통신이 가능하다.
  - FIFO라고 불리는 특수 파일을 서로 무관한 다른 프로세스들 사이의 통신에 사용하기에 외부 프로세스와 통신이 가능하다.
- 파이프와 같이 반이중 통신이다.
- 파이프와 같이 읽기, 쓰기를 동시에 수행할 수 없어 전이중 통신을 하기 위해선 FIFO 파일을 두개 만들어야 한다.

### 메시지 큐(Message Queue)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/IPC-Message-queue2.png' width='600'>
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/IPC-Message-queue.png' width='600'>

- FIFO 자료 구조를 가지는 큐를 이용해 데이터를 전송, 수신하는 방식으로 커널에서 관리한다.
- 입출력 방식은 Named PIPE와 동일하다.
- Named PIPE는 스트림(데이터 흐름)을 기반으로 작동하지만 메시지 큐는 흐름이 아닌 메모리 공간을 이용한다.
  - 메시지 또는 패킷 단위로 작동한다.
- PIPE나 FIFO와 달리 다수의 프로세스 간에 데이터 송/수신이 가능하다.
- 메시지 큐에 쓸 데이터에 번호를 붙여 다수의 프로세스가 동시에 데이터를 쉽게 다룰 수 있다.
- 전이중 통신(Full Duplex)이 가능하며, 메시지의 형태는 사용자가 정의할 수 있다.
- 비동기 방식이며 방대한 처리량이 있을 시 큐에 삽입 후 나중에 처리할 수 있다.
- 데이터가 쌓일 수록 추가 메모리 자원이 필요하며, 큐에 데이터를 삽입, 추출하는 과정에서 오버헤드가 발생할 수 있다.

### 소켓(Socket) 
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/IPC-Socket.png' width='600'>

> 소켓의 개념
> 
> 소켓은 네트워크 상에서 통신하기 위한 종단점으로 추상화된 개념  
> 소켓 통신은 네트워크 통신 기법으로 많이 사용되며 지정된 양쪽 임의의 포트를 통해 데이터를 주고 받는 방식  
> 소켓의 네트워크 기능을 통해 한 PC 내의 두 프로세스 간의 통신으로 사용이 가능하다. 

- 네트워크 소켓 통신을 통해 Client - Server 구조로 데이터 통신을 하며, 원격에서 프로세스 간 데이터를 공유할 때 사용한다.
  - 포트를 담당하는 프로세스를 양쪽에 각각 두어 데이터를 송수신하는 역할을 수행하도록 한다.
  - PC에서 프로세스를 통해 타 포트에 연결하라는 명령을 하면 두 프로세스는 서로 확인 과정을 거친 후 연결을 진행하고 1:1로 데이터를 주고 받는다.
  - 서버 단에서는 주소 할당(bind), 통신 요청 대기(listen), 통신 수락(accept)을 진행하여 소켓 연결을 위한 준비를 하고, 클라이언트 단에서는 통신 요청(connect)를 통해 서버에 요청하고 연결이 수립된 후, 소켓에 전송함으로써 데이터를 주고 받는다.
  - 포트의 도움으로, 다른 IPC와 달리 프로세스의 위치에 독립적이며, Machine Boundary와 관계가 없어 Local 또는 Remote로 사용할 수 있다.
  - 다른 IPC는 Local에서만 사용이 가능하다.
- 전이중 통신(Full Duplex)이 가능하다. 
- 패킷 단위로 주고 받기에 직관적으로 이해하기 쉬운 코드를 작성할 수 있지만 Internet UDP와 달리 경로를 지정할 수는 없다.
- 클라이언트/서버 환경을 구축하는데 용이하며, 중대형 어플리케이션에서 주로 사용한다. 

## 세마포어(Semaphore)
다른 IPC는 대부분 프로세스 간의 메시지 전송을 목적으로 하는 것에 반해, 세마포어는 프로세스 간의 데이터를 동기화하고 보호하는 것을 목적으로 한다.  
공유한 자원에 여러 개의 프로세스가 동시에 접근하면 안되는 경우, 한번에 하나의 프로세스만 접근이 가능하도록 할 때 사용한다.

## 정리
### 공유 메모리 모델과 메시지 패싱 모델의 장단점
- 공유 메모리 모델(Shared-memory Model)
  - 장점
    - 커널의 개입 없이 메모리를 직접 사용하여 통신하기에 어떤 IPC보다 통신 속도가 빠르다.
  - 단점
    - 동기화 문제가 발생할 수 있어 별도의 동기화 과정이 필요하다.
    - 동시에 같은 메모리 위치에 접근하는 문제가 발생할 수 있다
- 메시지 패싱 모델(Message-passing Model)
  - 장점
    - 커널에서 데이터를 주고 받는 과정을 컨트롤할 수 있어 안전하다.
    - send/receive 연산에 대해 커널이 동기화를 제공해준다.
  - 단점
    - 커널을 통해서 데이터를 주고 받기 때문에 통신 속도가 느리다. 

### IPC 정리
|종류|Shared Memory|Memory Map|PIPE|Named PIPE(FIFO)|Message Queue|Socket|Signal|
|:-:|:-----------:|:--------:|:--:|:--------------:|:-----------:|:----:|:----:|
|사용 시기|다른 프로세스와 양방향 통신시|다른 프로세스와 양방향 통신시|부모-자식 간 단방향 통신시|다른 프로세스와 단방향 통신시|다른 프로세스와 양방향 통신시|다른 시스템 간 양방향 통신시|다른 프로세스와 단방향 통신시|
|공유 매개체|메모리|메모리 + 파일|파일|파일|메모리|소켓|시그널(인터럽트)|
|통신 단위|구조체|페이지|스트림|스트림|구조체|스트림|시그널(인터럽트)|
|통신 방향|양방향|양방향|단방향|단방향|양방향|양방향|단방향|
|통신 가능 범위|동일 시스템|동일 시스템|동일 시스템|동일 시스템|동일 시스템|동일 + 외부 시스템|동일 시스템|


> ⬆️:[Top](#IPCInter-Process-Communication)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Operating-System)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [구현회. 운영체제-그림으로 배우는 구조와 원리, 개정3판. 한빛아카데미]
> - [[운영체제] IPC](https://steady-coding.tistory.com/508)
> - [IPC(Inter-Process Communication)](https://sepang2.tistory.com/45)
> - [Inter Process Communication - Pipes](https://www.tutorialspoint.com/inter_process_communication/inter_process_communication_pipes.htm)
> - [프로세스 간 통신](https://ko.wikipedia.org/wiki/%ED%94%84%EB%A1%9C%EC%84%B8%EC%8A%A4_%EA%B0%84_%ED%86%B5%EC%8B%A0)
> - [[OS] 프로세스 간 통신 방법(Inter Process Communication, IPC)](https://dar0m.tistory.com/233)
> - [프로세스간 통신(Interprocess Communication)](https://neos518.tistory.com/132)
