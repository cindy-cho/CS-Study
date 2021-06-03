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

* 동작
    * Hash Funtion을 이용하여 Key값을 Hash값으로 바꾼다
    * Hash 값을 Index로 하여 Value를 저장

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
        - 비어있는 공간을 활용하는 방법
        
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