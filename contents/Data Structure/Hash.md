# Hash
## HashTable의 개념
  - Key와 Value를 1:1로 연관지어 저장하는 자료구조(연관배열 구조)
  - Key를 Hash Function를 통해 Hash를 찾아 Value를 도출
    - 키 값 비교를 통한 검색이 아닌 산술적인 연산을 이용
## HashTable 기능
  - 연관배열 구조와 동일한 기능 지원
  - Key, Value가 주어질 때, 두 값을 저장
  - Key가 주어졌을 때, Key와 연결된 Value 조회
  - 기존 Key에 새로운 Value가 주어졌을 때, 기존 Value를 새로운 Value로 대체
  - Key가 주어졌을 때, 해당 Key에 연관된 Value 삭제
## HashTable 구조

  ![HashTable구조](https://github.com/Minho979/CS_Study/blob/main/contents/images/HashTable.png)

  - Key, Hash Function, Hash, Value, 저장소(Bucket, Slot)로 구성
  - Key
    - 고유의 값
    - 저장 공간의 효율성을 위해 Hash Function에 입력하여 Hash로 변경 후 저장
      - Key는 길이가 다양하여 그대로 저장할 시 다양한 길이만큼 저장소 구성이 필요
  - Hash Function
    - Key를 Hash로 바꾸주는 역할
    - 해시 충돌(서로 다른 Key가 동일한 Hash가 되는 경우)이 발생할 확률을 최대한 줄이는 함수를 만드는 것이 중요
    - Key들을 Hash Table에 골고루 분포 시킬 수 있도록 Hash를 계산이 필요
      - 빈 공간이 있는데 충돌이 발생하는 경우 오버플로우를 유발해 좋은 Hash Function이  아님
    - 계산이 쉽고 빨라야 함
      - Key 값의 비교 연산을 수행하는 시간보다 빨라야 Hash를 사용하는 의미가 있음
  - Hash
    - Hash Function의 결과
    - 저장소에서 Value와 매칭되어 저장
  - Value
    - 저장소에 최종적으로 저장되는 값
    - 키와 매칭되어 저장, 삭제, 검색, 접근 가능

## Hash Table 동작 과정
  1. Key -> Hash Function-> Hash = Hash Function 결과
  2. Hash를 배열의 Index로 사용
  3. 해당 Index에 Value 저장, 삭제 수행
     - HashTable 크기가 10일 시 A라는 Key의 Value를 찾을 때 HashFunction("A") % 10 연산을 통해 Index 값을 계산하여 Value 조회

## Hash 충돌 (Collision)
  - 서로 다른 Key가 Hash Function에서 중복 Hash가 나오는 경우
  - 충돌이 많아질수록 탐색 시간 복잡도가 O(1)에서 O(n)으로 증가

### Hash 충돌 해결 방법
  **1. Separating Chaining**
     
  - JDK 내부에서 사용하는 충돌 처리 방식
  - Linked List(data 6개 이하) 또는 Red-Black Tree(data 8개 이상) 사용

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/HashChaining.png" width="600">
      [⬆️ h(x) = x % 5의 경우 chaining]

  - Linked List 사용 시 충돌이 발생하면 충돌 발생한 Index가 가리키고 있는 Linked List 노드 추가하여 Value 삽입
  - Key에 대한 Value 탐색 시에는 인덱스가 가리키고 있는 Linked List를 선형 검색하여 Value 반환 (삭제도 동일한 방식으로 진행)
  - Linked List 구조의 특성상 추가 데이터 수 제약이 적음

 **2. Open addressing**
     
  - 추가 메모리 공간을 사용하지 않고, HashTable 배열의 빈 공간을 사용하는 방법
  - Separating Chaining 방식에 비해 적은 메모리 사용
  - Linear Probing, Quadratic Probing, Double Hashing 방식으로 나뉨

  <img src="https://github.com/Minho979/CS_Study/blob/main/contents/images/Linearopen.png" width="500">
       [⬆️ h(x) = x % 5의 경우 Linear Probing]

  - 충돌이 발생할 시 다음 버킷을 조사하는 방식으로 검색, 저장
    - 검색의 경우 다음 버킷이 비어있거나, 마지막 버킷에 도달한 경우 검색 실패
       
  **3. Resizing**
  - 저장 공간이 일정 수준 채워지면 Separating Chaining의 경우 성능 향상을 위해, Open addressing의 경우 배열 크기 확장을 위해 Resizing
  - 보통 2배로 확장
  - 확장 임계점은 현재 데이터 개수가 현재 Hash Bucket개수의 75%가 될 때

## Hash Table 장점
  - 적은 리소스로 많은 데이터를 효율적으로 관리 가능
    - ex. HDD, Cloud에 있는 많은 데이터를 Hash로 매핑하여 작은 크기의 캐시 메모리로 프로세스 관리 가능
  - 배열의 인덱스를 사용하기 때문에 빠른 검색, 삽입, 삭제 가능 (O(1))
    - Hash Table의 경우 인덱스는 데이터의 고유 위치이기 떄문에 삽입 삭제 시 다른 데이터를 이동할 필요가 없어 삽입, 삭제도 빠른 속도로 수행
  - Key와 Hash에 연관성이 없어 보안 유리
  - 데이터 캐싱에 많이 사용
    - get, put 기능에 캐시 로직 추가 시 자주 hit하는 데이터 바로 검색 가능
  - 중복 제거 유용

## Hash Table 단점
  - 충돌 발생 가능성
  - 공간 복잡도 증가
  - 순서 무시
  - 해시 함수 의존도

## HashTable vs HashMap
  - Key-Value 구조 및 Key에 대한 Hash로 Value를 관리하는 것은 동일
  - Hash Table
    - 동기
    - Key-Value 값으로 null 미허용(Why? Key가 hashcode(), equals()를 사용)
    - 보조 Hash Function과 Separating Chaining을 사용하여 비교적 충돌 가능성을 낮춤 (Key의 Hash 변형)
  - Hash Map
    - 비동기 (멀티 스레드 환경에서 사용시 주의)
    - Key-Value 값으로 null 허용

## Hash Table 성능
  ||평균|최악|
  |---|----|----|
  |탐색|O(1)|O(N)|
  |삽입|O(1)|O(N)|
  |삭제|O(1)|O(N)|

> ⬆️:[Top](#Hash)
> ⬅️:[Back](https://github.com/Minho979/CS_Study/blob/main/README.md#1-data-structure)
> 💁:[Home](https://github.com/Minho979/CS_Study/blob/main/README.md)
> - Reference
> - [이지영. 지바로 배우는 쉬운 자료구조. 한빛아카데미]
> - [문병로. 쉽게 배우는 알고리즘. 한빛아카데미]
