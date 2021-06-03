Algorithm
=============

Big O
-----

DFS와 BFS
-----
* DFS (Depth-First Search) : 깊이 우선 탐색
    * 사용 하는 경우 : 모든 노드를 방문하고자 하는 경우

* BFS (Breadth-First Search) : 너비 우선 탐색
    * 사용 하는 경우 : 최단 경로 혹은 임의의 경로를 찾는 경우


Fibonacci : 1 1 2 3 5 8 ...
-----
* 재귀를 이용한 구현
    * 시간 복잡도 : O(2^n)
```cpp
int Fibo(int n){
    if( n >= 2 ) return Fibo(n-1) + Fibo(n-2);
    return n;
}

int main(void){
    cout << Fibo(n) << endl;
    return 0;
}
```

* 반복을 이용한 구현
    * 시간 복잡도 : O(n)
```cpp
int main(void){
    if( n < 2 ){
        cout << n << endl;
        return 0;
    }
    int a=0, b=1
    for(int i=2 ; i<=n ; i++){
        a = a+b;
        swap(a,b);
    }
    cout << b << endl;
}
```

* DP를 이용한 구현
    * 반복을 이용한 구현
    ```cpp
    int main(void){
        if( n < 2 ){
            cout << n << endl;
            return 0;
        }
        vector<long long> DP(n+1);
        DP[0] = 0; DP[1] = 1;
        for(int i=2 ; i<=n ; i++)
            DP[i] = DP[i-1] + DP[i-2];
        
        cout << DP[n] << endl;
    }
    ```

정렬 알고리즘
-----

Greedy
-----

MST
-----

Kruskal MST
-----

Prim MST
-----
