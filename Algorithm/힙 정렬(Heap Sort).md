# 힙 정렬(Heap Sort)

완전 이진 트리를 기본으로 하는 힙 자료구조를 기반으로 한 정렬 방식

- 최악의 경우 시간복잡도 O(nlog2n)

- Sorts in place - 추가 배열 불필요

- 이진힙(binary heap) 자료구조를사용

## 과정

1. 최대 힙을 구성
2. 현재 힙 루트는 가장 큰 값이 존재함. 루트의 값을 마지막 요소와 바꾼 후, 힙의 사이즈를 하나 줄임
3. 힙의 사이즈가 1보다 크면 위 과정 반복





Java Code

```java
private void solve() {
    int[] array = { 230, 10, 60, 550, 40, 220, 20 };
 
    heapSort(array);
 
    for (int v : array) {
        System.out.println(v);
    }
}
 
public static void heapify(int array[], int n, int i) {
    int p = i;
    int l = i * 2 + 1;
    int r = i * 2 + 2;
 
    if (l < n && array[p] < array[l]) {
        p = l;
    }
 
    if (r < n && array[p] < array[r]) {
        p = r;
    }
 
    if (i != p) {
        swap(array, p, i);
        heapify(array, n, p);
    }
}
 
public static void heapSort(int[] array) {
    int n = array.length;
 
    // init, max heap
    for (int i = n / 2 - 1; i >= 0; i--) {
        heapify(array, n, i);
    }
 
    // for extract max element from heap
    for (int i = n - 1; i > 0; i--) {
        swap(array, 0, i);
        heapify(array, i, 0);
    }
}
 
public static void swap(int[] array, int a, int b) {
    int temp = array[a];
    array[a] = array[b];
    array[b] = temp;
}
```


## 시간복잡도

**최선**: Ω(nlogn)
**평균**: Θ(nlogn)
**최악**: O(nlogn)
		
## 공간복잡도

O(n)


## 장점

- 가장 크거나 가장 작은 값을 구할 때
  > 최소 힙 또는 최대 힙의 루트 값이기 때문에 한 번의 힙 구성을 통해 구하는 것이 가능

- 최대 k만큼 떨어진 요소들을 정렬할 때
  > 삽입정렬보다 더욱 개선된 결과를 얻어낼 수 있음

## 단점

- 불안정 정렬

- 퀵정렬과 합병정렬의 성능이 좋기 때문에 힙 정렬의 사용빈도가 높지는 않음

