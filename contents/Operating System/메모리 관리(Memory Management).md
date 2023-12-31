# 메모리 관리(Memory Management)
메모리는 프로세서가 실행할 프로그램 코드와 데이터를 저장하는 물리 장치로 레지스터, 캐시 메모리, 메인 메모리, 보조 기억 장치 등 일고 쓰는 속도와 용량에 따라 메모리 계층 구조를 이룬다.

## 메인 메모리 
- 일반적으로 프로세서는 메인 메모리에 직접 접근하여 처리할 내용을 가져오고, 메인 메모리에 처리 결과를 저장한다.
- 프로세서는 레지스터가 가리키는 주소로 메모리에 접근하여 다음에 수행할 명령어를 가져온다. 필요한 데이터가 없을 시 MMU를 통해 데이터를 가져온다.
- 프로세스가 정상적으로 실행되기 위해서 프로그램이 메모리에 적재되어야 한다.
- 기본 단위는 바이트(byte) 또는 워드(word)를 사용한다.
- 주소가 할당된 일련의 바이트들로 구성되어 있다.

## 메모리 관리 
- 운영체제는 동적으로 메인 메모리를 관리한다.
  - 프로세스들을 위해 메모리 할당, 제거, 보호를 수행한다.
- 메인 메모리는 운영체제를 위한 영역과 실행 중인 프로그램을 위한 사용자 영역으로 구분된다.
- 다중 프로그래밍 시스템에서는 사용자 영역을 여러 프로세스가 사용하도록 세분화 해야 한다.

## 메모리 관리 정책
### 반입 정책(fetch strategy)
- 적재 정책이라고도 불린다.
- 디스크에 있는 프로세스를 메인 메모리에 로드할 시기를 결정하는 방법이다.
- 요구 반입(demand fetch): 요청이 있을 때 반입하는 방법
- 예상 반입(anticipatory fetch): 예측을 통해 요구가 없어도 미리 반입하는 방법
### 배치 정책(placement strategy)
- 디스크에서 반입한 프로세스를 메인 메모리의 빈 공간 중 어디에 저장할 것인가를 결정하는 방법이다.
- 최초 적합(first-fit), 최적 적합(best-fit), 최악 적합(worst-fit)
### 교체 정책(replacement strategy)
- 대치 정책이라고도 불린다.
- 메인 메모리가 부족하여 새로 로드할 프로세스를 놓을 공간이 없는 경우, 기존에 메인 메모리를 차지하고 있던 어떤 부분을 제거할 것인지 결정하는 방법이다.

## 메모리 구조와 매핑
### 메모리 해석 두 가지 관점
#### 논리적 주소 공간(logical address space)
- 프로그램이 사용하는 주소로 이루어진 메모리 공간
- 논리적 공간 크기는 각 시스템에서 정의한 워드 길이에 따라 다르다.
  - 예) 32비트 시스템: $2^{32}$ byte
- 주소로 구분할 수 있어야 실제 주소 공간을 설정할 수 있다.
- 주소를 지정할 수 없으면 프로그램 A가 표현할 수 있는 논리적 공간이 아니다.
#### 물리적 주소 공간(physical address space)
- 데이터나 프로그램이 저장되는 실제 메모리 공간이다.
- 논리적 공간보다 크거나 작을 수 있다.

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Management-physical-address.png' width='500'>
  
  - 반드시 0, 1, 2에 매핑될 필요 없으며 저장할 수 있는 빈 공간에 매칭되어 저장한다.
  - 0 → 30(논리적 → 물리적)으로 신속하게 주소 변환하여 매핑이 된다. 
### 메모리 장치의 주소 변환
#### MMU(Memory Management Unit)
<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Management-MMU.png' width='500'>

- 메모리 보호나 캐시 관리 등 프로세서가 메모리에 접근하는 것을 관리하는 하드웨어이다. 
- 논리 주소를 물리 주소로 변환한다.
- 주소 변환 기법은 메모리 관리 방식에 따라 달라진다.
  - 연속 메모리 할당: 고정 분할, 가변 분할(동적 분할)
  - 불연속 메모리 할당: 페이징(paging), 세그먼테이션(segmentation), 페이지화된 세그먼테이션

- 예) base register을 더해 물리 주소로 변환하는 예시

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Management-MMU-ex1.png' width='500'>
  
  - base register : 접근할 수 있는 물리적 주소의 최솟값
  - limit register : 논리적 주소의 범위

### 주소 바인딩
- 프로세서가 프로세스를 실행하기 위해 프로세스의 논리적 주소에 해당하는 물리적 주소를 정해준다.
- 프로그램의 주소를 절대 주소로 바꾸어 메인 메모리에 적재할 수 있도록 한다.
- 바인딩하는 시점에 따라 구분된다.

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Management-binding.png' width='500'>

#### 컴파일 시간(compile-time) 바인딩
- 컴파일 시 프로세스의 물리적 주소를 결정한다.
- 메모리 내 프로세스 위치를 미리 알고있다면, 컴파일러가 해당 위치에 고정된 주소(절대 주소)를 생성한다.
- 논리적 주소와 물리적 주소가 동일하다.

#### 적재 시간(load-time) 바인딩
- 메모리 내 프로세스의 위치를 알 수 없는 경우 컴파일러는 재배치 가능한(relocatable) 상대 주소를 생성한다.
- 상대 주소는 프로그램 시작 주소가 0이므로, 최종 바인딩(절대 주소 결정)을 적재시간까지 연기한다.
- 프로세스를 메모리에 load하는 시점에 로더(loader)가 물리적 주소를 결정한다.
- 논리 주소와 물리 주소가 다를 수 있다.
> 로더(loader): 외부 기억장치로부터 정보들을 주기억 장치로 옮기기 위해 메모리 할당(allocation) 및 연결(linking), 재배치(relocation), 적재(loading)를 담당

#### 실행 시간(run-time) 바인딩
- Execution Time 바인딩이라고도 불린다.
- 프로그램이 실행 도중 메모리 상의 위치가 변하는 경우, 바인딩을 실행시간까지 연기한다.
- 프로세스 실행 시 메모리 주소를 동적으로 변경하는 방법이다.
- 런타임 시 물리적 주소가 결정된다.
- 런타임 주소 할당은 MMU라는 장치를 사용해서 논리 주소를 물리 주소로 바꾼다.

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Management-runtime.png' width='500'>

## 메모리 관리 관련 용어
### 동적 적재(dynamic loading)
- 실행되기 직전에 주소를 확정하여 메모리를 효율적으로 사용하게 하는 방법이다.
- 사용하지 않는 루틴은 메모리에 로드하지 않으므로 프로그램이 큰 경우 유용하다.

#### 동작
- 모든 루틴은 실행 시간에 호출될 때까지 메모리 내에 로드되지 않고 재배치 가능한 형태로 디스크에 저장된다.
- 메인 루틴만 먼저 메모리에 로드하여 실행한다.
- 메인 루틴이 다른 루틴을 호출할 때, 호출된 루틴이 메모리에 로드되어 있는지를 조사한다.
- 로드되어 있지 않다면 호출될 루틴을 메모리에 적재하고 프로그램의 주소 테이블을 갱신한다.

### 중첩(overlay)
- 메인 메모리보다 더 큰 프로그램을 실행할 수 있도록하는 기법이다.
- 중첩을 이용학려면 프로그래머가 중첩 구조를 직접 설계하고 프로그래밍해야 한다.
- 중첩은 운영체제의 지원 없이도 실행이 가능하다.

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Management-overlay.png' width='500'>

#### 동작
- 메모리 일부분에 프로그램 실행 중 계속 필요한 사용자 코드와 데이터를 로드한다.
- 중첩 영역에는 초기 모듈, 처리 모듈, 출력 모듈을 순서대로 하나씩 로드하여 실행한다.
- 전체를 로드할 메모리 공간은 없으나 일부를 로드할 공간이 있다면 중첩 영역에 일부 로드하여 실행한다. 

### 스와핑(swapping)
- 메모리 크기가 제한적이기에 프로세스를 디스크에 이미로 내보내고 필요할 때 메모리에 다시 로드하는 경우 사용하는 기술이다. 
- 즉, 프로세스가 메인 메모리에 계속 머물지 않도록 하는 기술이다.
- 스케줄러를 통해 어떤 프로세스를 `swap in/out` 할지를 결정한다.
  - `swap out`: 프로세스가 메모리를 차지하고 실행하다가 프로세서를 사용하지 않을 때에는 메모리를 내어 준다.
  - `swap in`: 실행을 위해 다시 메모리에 올라온다.
- 컴파일 시간 바인딩과 적재 시간 바인딩은 `swap in`할 때 같은 메모리 위치로 로드해야한다.
- 실행 시간 바인딩의 경우 주소 변환이 되기 때문에 빈 메모리 영역이라면 로드할 수 있다. 

  <img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Management-swapping.png' width='500'>

### TLB (Translation Look-aside Buffer)
- TLB는 메모리 주소 변환을 위한 별도의 캐시 메모리로, page table에서 빈번히 참조되는 일부 엔트리를 캐싱한다.
- TLB는 key-value 쌍으로 데이터를 관리하며, key에는 page number, value에는 frame number가 대응된다.
- 따라서 CPU는 TLB를 page table 보다 먼저 참조하여, 원하는 페이지가 있다면 바로 frame number를 얻을 수 있다.

<img src='https://github.com/Minho979/CS_Study/blob/main/contents/images/Memory-Management-TLB.png' width='500'>


> ⬆️:[Top](#메모리-관리Memory-Management)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#%EF%B8%8F-Operating-System)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [구현회. 운영체제-그림으로 배우는 구조와 원리, 개정3판. 한빛아카데미]
> - [[운영체제(OS)] 8. 메모리 관리(Memory Management)](https://rebro.kr/178)
