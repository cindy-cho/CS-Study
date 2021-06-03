Data Structure
=============
Array
-----
Linked List
-----------
HashTable : (Key, Value)로 데이터를 저장하는 자료구조
---------
* 개념
    * Key와 Value를 1:1로 matching 하여 저장하는 자료구조
    * Key
        * 고유한 값
        * Hash Function을 이용해 Hash로 변경 후 저장한다
    * Hash
        * Hash Function의 결과
        * 저장소에서 Value와 매칭되어 저장

* 시간 복잡도
    |     | avg |worst|
    |-----|-----|-----|
    | 탐색 | O(1)| O(N)|
    | 삽입 | O(1)| O(N)|
    | 삭제 | O(1)| O(N)|

* 동작
    * Hash Funtion을 이용하여 Key값을 Hash값으로 바꾼다
    * Hash 값을 Index로 하여 Value를 저장

* 장점
    * 적은 리소스로 많은 데이터를 효율적으로 관리
    * 빠른 검색, 삽입, 삭제 : O(1) - 배열의 인덱스 사용
    * 보안에 유리 - Key와 Hash
    * 중복 제거에 유용
    * 데이터 캐싱에 주로 사용

* 단점
    * 충돌 발생 가능성
    * 공간 복잡도 증가
    * 순서 무시
    * 해시 함수 의존

* Hash Table // Hash Map
    * 공통점
        * (Key, Value) 구조
    * Hash Table
        * 동기
        * NULL 값 허용
        * 보조 Hash Fucntion과 Seperating Chaining을 사용하여 해시 충돌 적음
    * Hash Map
        * 비동기 - 멀티 스레드 환경에서 유의
        * NULL 값 미 허용 : hashcode(), equals() 사용하기 때문

* Hash 충돌
    * Key의 Hash값이 중복 되는 경우
    * 중복이 많을수록 탐색 시간 복잡도 증가 : O(1) -> O(N)

* Hash 충돌 해결방법
    * Seperating Chaining (분리 연결법)
        * Linked List, Red-Black Tree
        * 동일한 Hash Bucket에 대해서 추가 메모리를 사용하여 저장
        * 장점 : 해시 테이블 확장 없이 간단하게 구현 가능
        * 단점 : 데이터의 수가 많아지면 효율성이 감소
    * Open Addressing (개방 주소법)
        * 비어있는 공간을 활용하는 방법
        * Linear probing, Quadratic Probing, Double Hashing Probing
        
Stack
-----
Queue
-----
Graph
-----
Tree
----
Binary Heap
-----------
Red-Black Tree
--------------
B+ Tree
-------