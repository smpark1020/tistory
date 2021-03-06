Heap이란 최대값이나 최소값을 찾아내는 연산을 빠르게 하기 위해 고안된 완전 이진 트리를 기본으로 한 자료구조이다.   
Heap에는 Max Heap(최대힙), Min Heap(최소힙) 2가지가 있다.   
Min Heap(최소힙)은 작은 값을 항상 위의 노드에 있게 해서 트리의 루트에는 가장 작은 값이 오게 하는게 Heap이다.   
Max Heap(최대힙)은 가장 큰 값이 맨 위에 오도록 모든 노드들은 부모 노드에 자기보다 큰 값을 가지는 트리구조이다.   

## Min Heap(최소힙)에 노드 삽입하기
1. 완전 트리의 맨 끝에 노드를 추가하는데 완전 이진 구조를 잃지 않도록 마지막 레벨의 왼쪽부터 채운다.   
(추가한 직후에는 데이터가 트리안에서 정렬이 되어있지 않은 상태이다.)
2. 자신의 부모노드와 값을 비교하여 자신이 더 작은 값이면 부모 노드와 자리를 바꾼다.   
3. 이렇게 계속 부모노드의 값이 자신보다 작을때까지 반복한다. (루트에 도착하면 멈춘다.)

이 과정은 균형이 맞춰진 완전 이진 트리에서 이루어지니까 한 레벨씩 루트까지 올라간다면 O(logn)의 시간복잡도를 갖게 된다.   

## Min Heap(최소힙)에서 노드 꺼내오기
Min Heap(최소힙)에 노드를 요청할 때는 가장 작은 값을 요청하게 된다.   
Min Heap(최소힙)에서 가장 작은 값은 루트에 있으니 가져오는 것은 매우 쉽다.   
하지만 루트를 가져온 이후에는 루트의 값이 비기 때문에 다시 값을 채워줘야 한다.   
그래서 완전 이진 트리의 맨 마지막 노드를 루트에 채운다.   
하지만 이 노드는 정렬이 안되어 있는 상태이다.   
따라서 이 노드는 자식 노드들과 비교해서 자식 노드들 중에 가장 작은 노드와 자리를 바꾼다.   
자식 노드들이 모두 자신보다 크거나 리프 노드까지 올때까지 이 과정을 반복한다.   
이 과정은 최대 O(logn)의 시간복잡도가 걸린다.   

> Max Heap(최대힙)은 Min Heap(최소힙)과 최대/최소만 다르고 같은 원리이므로 설명을 생략한다.   

## 참고
* [[자료구조 알고리즘] Binary Heaps (Min-Heaps and Max-Heaps)](https://youtu.be/jfwjyJvbbBI)