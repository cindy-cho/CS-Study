Data Structure
=============
Array
-----
Linked List
-----------
HashTable
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
    * Hash Funtion을 이용하여 Key값을 Hash값으로 바꾼다.
    * Hash 값을 Index로 하여 Value를 저장한다.

* Hash 충돌
    * Key의 Hash값이 중복 되는 경우
    * 중복이 많을수록 탐색 시간 복잡도 증가 : O(1) -> O(N)

* Hash 충돌 해결방법
    * Seperating Chaining
        * JDK 내부에서 사용하는 충돌 처리 방식
            * 데이터 6개 이하 : Linked List
            * 데이터 8개 이상 : Red-Black Tree

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