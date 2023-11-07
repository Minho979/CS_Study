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
- 공유 메모리 모델(Shared-memory Model): Shared Memory, Memory Map
- 메시지 패싱 모델(Message-passing Model): Signal, PIPE, FIFO, Message Queue, Socket, Semaphore

## 공유 메모리 모델(Shared-memory Model)
- 프로세스 간 공유 메모리 영역을 설정하고 공유 영역에서 데이터를 읽고 쓰는 방식으로 데이터를 교환한다.
- 시스템 호출이 메모리 생성 및 제거할 때에만 필요하기 때문에 커널이 개입이 적어, 메세지 패싱 모델보다 빠르다.
- 프로그램 레벨에서 통신 기능을 제공하여 자유로운 통신이 가능하다.
- 공유 메모리로 인한 동기화 문제가 발생할 수 있다. 

### 공유 메모리(Shared Memory)
- 한 시스템 내에 있는 프로세스들에 한에서만 공유되며 프로세스 중 하나가 공유 메모리를 생성하면 다른 프로세스들은 해당 공유 메모리를 읽거나 쓸 수 있다.
- 공유 메모리가 각 프로세스에게 첨부(attach)하는 방식으로 작동하게 된다.
- 대량의 정보를 다수의 프로세스에게 배포 가능하다.
- 중개자 없이 곧바로 메모리에 접근할 수 있기에 모든 IPC 중에서 가장 빠르게 작동할 수 있다. 

### 메모리 맵(Memory Map)
- 공유 메모리처럼 메모리를 공유하지만 열린 파일을 메모리에 매핑 시켜서 공유하는 방식이다.
  - 공유 매개체: 파일 + 메모리
- 주로 파일로 대용량 데이터를 공유해야 할 때 사용한다.
- FILE IO가 느릴 때 사용한다.
- 대부분 프로세스를 실행할 때 실행 파일의 각 세그먼트 메모리에 사상하기 위해 메모리 맵 파일을 이용한다.
- 메모리 맵 파일은 파일의 크기를 바꿀 수는 없으며 메모리 맵 파일을 사용하기 이전, 또는 이후에만 파일의 크기를 바꿀 수 있다. 

## 메시지 패싱 모델(Message-passing Model)

### 시그널(Signal)
### 익명 파이프(PIPE)

### Named PIPE(FIFO)

### 메시지 큐(Message Queue)
### 소켓(Socket) 

### 세마포어(Semaphore)

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
