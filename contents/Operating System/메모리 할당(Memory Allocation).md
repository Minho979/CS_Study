# 메모리 할당(Memory Allocation)
운영체제가 새 프로세스를 실행시키거나 실행중인 프로세스가 메모리를 필요로 할 때 물리 메모리를 할당하는 것으로 운영체제 커널에 의해 이루어진다.  
방식에는 연속 메모리 할당(Contiguous Memory Allocation)과 분할 메모리 할당(Non-contiguous Memory Allocation)이 있다.

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation.png' width='600'>

## 연속 메모리 할당(Contiguous Memory Allocation)
- 초기 컴퓨터 시스템의 메모리 관리 기법으로 프로세스 1개에 연속된 메모리 블록을 할당하는 기법이다. 
- 프로세스에 하나의 연속된 메모리를 할당하므로 메모리 할당의 유연성이 부족하다. 
- 프로그램이 메모리보다 큰 경우 실행이 불가능하므로 프로그램을 수정하거나 작은 모듈로 구성해야 한다.

### 할당 방식
- [단일 프로그래밍 환경의 연속 메모리 할당](#단일-프로그래밍-환경의-연속-메모리-할당)
- [다중 프로그래밍 환경의 연속 메모리 할당](#다중-프로그래밍-환경의-연속-메모리-할당)
  - [고정 분할 다중 프로그래밍](#고정-분할-다중-프로그래밍)
  - [가변 분할 다중 프로그래밍](#가변-분할-다중-프로그래밍)
- [버디 시스템(buddy system)](#버디-시스템buddy-system)

## 분할 메모리 할당(Non-contiguous Memory Allocation)
- 단편화로 인한 메모리 낭비를 줄이기 위해 고안된 방법이다.
- 연속 메모리 할당과 달리 하나의 프로세스를 메인 메모리에 분산하여 불연속적으로 할당할 수 있게 허용하여 분산 할당한다. 

### 할당 방식
- 고정 분할: [페이징(paging)](#페이징paging)
- 가변 분할: [세그먼테이션(segmentation)](#세그먼테이션segmentation)
- 고정 분할 + 가변 분할: [페이지화된 세그먼테이션(pageed segmentation)](#페이지화된-세그먼테이션pageed-segmentation)

## 단편화
- 프로세스에게 할당할 수 없는 작은 크기의 홀(hole, 조각 메모리)이 생기는 현상이다.
- 프로세스들이 메모리에 적재되고 제거되는 일이 반복되면, 프로세스들이 차지하는 메모리 틈 사이사이에 빈 공간들이 늘어나서 발생한다.
- 홀이 생기는 위치에 따라 내부 단편화와 외부 단편화로 나뉜다.
### 내부 단편화(internal fragmentation)
- 프로세스에게 할당된 메모리 영역 내에 활용할 수 없는 홀이 생기는 경우이다.
- 할당받은 공간보다 프로세스가 더 작으면, 낭비되는 메모리가 생기는 현상이다.
- 고정 크기 할당에서 발생한다.

- 예)
  
  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-fixed-internal.png' width='300'>

### 외부 단편화 (External Fragmentation)
- 할당된 메모리 사이에 활용할 수 없는 홀이 생기는 경우이다.
- 메모리 전체 빈 공간 양은 충분하더라도 너무 작은 공간들로 나누어져 있어서 어느 프로세스의 요구도 들어줄 수 없는 상태이다.
- 크기가 서로 다른 프로세스들이 연속된 메모리를 할당받고 반납하는 과정이 반복되며 사용가능공간이 여러 개의 작은 공간(hole)로 단편화 될 수 있다.

- 예)

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-variable-external.png' width='600'>
  
- 해결 방법
  - 메모리 통합(coalescing)
    - 하나의 작업이 끝났을 때 반납할 hole이 다른 hole과 인접한지를 검사하여 인접한 경우 hole을 하나로 합친다.
    - 메모리 통합을 수행하더라도 메모리 전반에 흩어져 있는 hole들을 모두 하나의 사용가능공간으로 합치기는 어렵다.
   
    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-variable-coalescing.png' width='500'>
    
  - 메모리 압축(compaction)
    - 사용 중인 메모리 공간의 내용들을 적절히 이동하여 사용가능 공간을 하나의 큰 hole로 모은다.
    - 동적(실행 시간) 주소 재배치가 가능한 경우에만 이용이 가능하다.
    - 메모리 압축 과정에서는 모든 작업을 중지해야 한다.
    - 압축 방법에 따라 이동량에 차이가 있다.

    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-variable-compaction.png' width='350'>  
 
    <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-variable-compaction1.png' width='600'>

## 단일 프로그래밍 환경의 연속 메모리 할당
- 사용자 프로세스가 1개인 경우이다.
- 메모리 영역을 운영체제를 위한 공간과 사용자 프로그램을 위한 공간으로 구분한다.
- 한 번에 한 프로세스만 메모리 사용이 가능하다.

#### 구조
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-single.png' width='350'>

#### 메모리 보호 기법
사용자 프로세스가 운영체제 영역에 접근하는 것을 막기 위해 프로세서 내에 경계 레지스터(boundart register)를 두고, 사용자 프로세스가 메모리를 참조할 때마다 경계 레지스터로 주소를 검사한다.

- 예) 경계 레지스터 값 = 100, 사용자 프로세스 = 80  
  경계 레지스터 값보다 100보다 작다. 이 경우 사용자라 프로세스가 운영체제 영역을 침범하기에 할당하지 않는다.

## 다중 프로그래밍 환경의 연속 메모리 할당
사용자 프로세스가 메모리에 여러 개가 적재된다.

### 고정 분할 다중 프로그래밍
- 메모리를 여러 개의 고정된 크기로 분할로 나누고, 각 분할에 프로세스에 하나씩 할당하는 방법이다.

#### 구조 
- 각 영역별로 독립된 큐가 있는 경우

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-fixed-queue.png' width='500'>

  - 할당된 공간이 정해진다.
  - if Q2 → 2KB, Q6 → 6KB, Q12 → 12KB 

- 통합된 대기 큐가 있는 경우

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-fixed-queue1.png' width='500'>

  - 어느 곳이든 할당 가능하다.
  - if 5KB → 12KB, 7KB → 12KB .. 등  할당될 공간이 정해져있지 않다.

#### 메모리 보호 기법
- 프로세서가 생성한 모든 주소를 기준 레지스터, 한계 레지스터로 검사하여 다른 사용자 프로그램과 운영체제를 보호한다. 
- 기준 레지스터 한계 레지스트를 사용하여 분할된 영역을 보호한다.
  - 기준 레지스터(base register): 분할 시작 물리 메모리 주소
  - 한계 레지스터(limit register): 분할의 크기

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-fixed-memory.png' width='300'>
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-fixed-memory1.png' width='500'>

#### 성능에 영향을 미치는 결정 사항
- 분할 영역의 개수와 크기 결정
- 프로세스를 어느 영역에 배치하는 결정

#### 단점 
- 고정된 분할보다 큰 프로세스는 실행이 불가능하다.
- 내부 단편화(internal fragmentation) 문제가 발생한다.

### 가변 분할 다중 프로그래밍
- 고정된 경계를 없애고 프로세스가 필요로 하는 만큼 메모리를 할당한다.

#### 가변 분할 동작)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-variable-ex.png' width='600'>

#### 메모리 보호 기법
- 각 프로세스(분할 영역)을 나타내기 위해 기준 레지스터, 한계 레지스터를 사용한다.
  - 기준 레지스터(base register): 프로세스의 메모리 시작 주소
  - 한계 레지스터(limit register): 프로세스의 크기 
- 프로세서 스케줄러가 프로세스 선택 시, 디스패처는 기준, 한계 레지스터에 새로운 값을 로드한다. 

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-variable.png' width='600'>

  - P3의 경우, 한계 레지스터 250, 기준 레지스터 5034, 물리적 주소 5034, 물리메모리 5034~5284  
    if 논리적 주소가 100인 경우 오류가 발생하지 않음  
    but 논리적 주소가 한계 레지스터보다 큰 경우 주소 오류가 발생함

#### 배치 정책(placement strategy)
- 가변 분할 다중 프로그래밍 시스템에서는 메모리 할당과 반납을 반복하다 보면 크기가 다양한 여러 빈 공간(hole)이 메모리에 생긴다.
- 요구한 크기의 메모리를 어느 공간(hole)에 할당할지를 결정해야한다. 
- 최초 적합(first-fit), 최적 적합(best-fit), 최악 적합(worst-fit) 세 가지의 배치 정책이 있다. 
- 일반적으로 최초 적합, 최적 적합이 최악 적합보다 효율적이다.
- 최초 적합이 최적 적합보다 메모리를 더 빠르게 할당한다. 

#### 최초 적합(first-fit)
- 사용가능공간 리스트에서 프로세스가 요구한 크기 이상인 첫번째 hole을 할당한다.
- 리스트의 처음부터 검색하거나 지난번 검색을 마친 곳부터 검색한다.
- 검색은 빠르나 공간 활용률이 떨어진다.

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-variable-first.png' width='500'>

#### 최적 적합(best-fit)
- 사용가능공간 리스트에서 프로세스가 요구한 크기 이상인 hole들 중에서 가장 작은 hole을 할당한다.
- 사용가능공간 리스트를 hole 크기 오름차순으로 유지해야 하며, 오름차순으로 정렬되어 있지 않은 경우 전체 리스트를 검색해야 한다.
- 공간 활욜률이 뛰어나지만 할당, 반납 시간이 오래 걸린다.
- 매우 작은 hole들이 생성될 수 있다.

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-variable-best.png' width='500'>

#### 최악 적합(worst-fit)
- 사용가능공간 리스트에서 가장 큰 hole을 할당한다.
- 사용가능공간 리스트를 hole 크기 내림차순으로 유지해야하며, 내림차순으로 정렬되어 있지 않은 경우 전체 리스트를 검색해야 한다.
- 매우 작은 hole들이 생기는 문제는 없지만, 매우 큰 hole이 남아 있지 않는다는 문제가 있다. 

#### 단점
- 외부 단편화(external fragmentation) 문제가 발생한다.

## 버디 시스템(buddy system)
- 고정 분할과 가변 분할의 단편화 현상을 해결하는 방법
- 큰 버퍼 들을 요청에 맞게 이등분하여 작은 버퍼들을 얻고, 가능할 때마다 이등분 되었던 인접한 빈 버퍼들을 합치는 과정을 반복한다.
- 이 때, 한 버퍼를 나누어 얻은 두 버퍼를 서로의 버디라고 한다.  

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Allocation-Contiguous-multi-variable-buddy.png' width='650'>

## 페이징(paging)
- 메모리를 일정한 크기의 페이지로 나누어 처리한다.
  - 메인 메모리(물리 메모리): 페이지 프레임(page frame)이라 불리는 고정 크기 블록으로 나눈다.
  - 프로세스 논리 메모리: 페이지(page)라 불리는 고정 크기 블록으로 나눈다. 페이지의 크기는 페이지 프레임과 동일하다.
- 프로세스 논리 메모리의 각 페이지가 메인 메모리의 어느 위치에 놓였는지를 찾을 수 있어야 한다.
- 프로세스마다 페이지 테이블(page table, page map table)을 가진다.
- 페이지의 개수는 페이지 테이블의 항목 수와 같다. 
- 페이지 크기를 줄이면 내부 단편화의 크기를 줄 일 수 있다.
- 페이지 크기를 줄이면 페이지 테이블이 커져 메모리를 많이 차지하며 매핑이 복잡해진다.

### 페이지 테이블
각 페이지가 몇번 프레임에 로드되었는지를 기록해둠으로써, 논리 페이지 번호를 알면 물리 페이지 프레임 번호를 알아낼 수 있도록 한다. 

#### 페이지 테이블 구성

#### 페이지 테이블 항목 PTE(Page Table Entry)

#### 페이지 테이블 구현 방법
- 전용 레지스터를 사용하여 페이지 테이블을 구현하는 방법
  - 페이지 테이블의 각 항목을 전용 레지스터에 저장한다.
  - 페이지 주소 변환이 매우 빠르다.
  - 페이지 테이블 크기가 작은 경우 사용할 수 있다. 
- 페이지 테이블을 메인 메모리에 유지하는 방법
  - 대부분의 시스템에서 페이지 테이블이 크기에 전용 레지스터로 구현하는 것이 적합하지 않다.
  - 페이지 테이블을 메인 메모리에 두고, 페이지 테이블 기준 레지스터(PTBR, Page Table Base Register)가 실행 중인 프로세스의 페이지 테이블을 가리키도록 한다. 

#### 페이지 주소 변환 방식 
**직접 매핑(direct mapping)**

- 페이지 테이블의 모든 항목들을 메인 메모리에 구현한다.
- 매핑 과정으로 인해 메모리 접근 시간(access time)이 길어진다.
- 하나의 메모리 워드에 접근하려면, 두 번의 메모리 접근(페이지 테이블 접근, 메모리 워드 접근)이 필요하다.
- 논리적 주소를 물리주소로 변환하는 과정)

**연관 매핑(associative mapping)**

- 연관 레지스터(associative register) 또는 변환 우선참조 버퍼(TLB, Translation Look-aside Buffers)로 페이지 테이블을 구현한다.
  - 연관 레지스터는 <key, value> 쌍을 저장히고, 모든 키를 동시에 비교하여 키가 발견되면 대응하는 값 부분을 출력하므로 빠른 탐색이 가능하다.
- 연관 레지스터에 <페이지 번호, 페이지 프레임 번호>를 저장하여 페이지 번호로부터 프레임 번호를 빨리 얻을 수 있게 하여 직접 매핑 메인 메모리 추가 접근 문제해결한다. 
- 페이지 테이블 기준 레지스터(PTBR)는 불필요하다.
- 주소 변환 속도는 매우 빠르지만, 연관 메모리 하드웨어가 비싸다.
- 시스템의 모든 프로세스들의 페이지 테이블 항목을 저장할 만큼 충분한 연관 레지스터를 갖추기 어렵다.
- 논리적 주소를 물리주소로 변환하는 과정)

**연관/직접 매핑 결합**


### 논리 주소 물리 주소 매핑(변환)

### 공유 페이지

### 메모리 보호

### 다중 단계 페이징(multi-level-paging) 시스템

### 장점
- 빈 페이지 프레임을 어떤 프로세스의 어떤 페이지도 사용할 수 있으므로 효율적인 메모리 사용이 가능하다.
- 연속되어 저장되지 않기 때문에 외부 단편화가 발생하지 않는다.
- 배치(placement) 전략이 따로 필요 하지 않다.
- 할당과 해제가 빠르다.
- [swap out](<https://github.com/Minho979/CS_Study/blob/main/contents/Operating%20System/메모리%20관리(Memory%20Management).md#스와핑swapping>)이 간단하다.

### 단점
- 연속 메모리 할당 방식에 비해 운영체제의 메모리 관리 부담이 커진다.
- 페이지 테이블을 위한 메모리가 추가로 소모된다.
- 고정된 크기의 페이지 프레임 단위로 할당하므로 내부 단편화 발생한다.
  - 페이지 크기를 줄여 해결이 가능하지만 페이지 테이블이 차지하는 메모리가 커지며 매핑이 복잡해진다.
- 페이지 테이블이 메모리에 있기 때문에 접근하는 연산은 2번의 메모리 접근이 필요하게 되어 속도가 느리다.
  - [TLB](<https://github.com/Minho979/CS_Study/blob/main/contents/Operating%20System/메모리%20관리(Memory%20Management).md#tlb-translation-look-aside-buffer>) 사용을 통해 속도를 향상시킨다.

### 페이징 시스템 요약

## 세그먼테이션(segmentation)
## 페이지화된 세그먼테이션(pageed segmentation)


> ⬆️:[Top](#메모리-할당Memory-Allocation)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Operating-System)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [구현회. 운영체제-그림으로 배우는 구조와 원리, 개정3판. 한빛아카데미]
