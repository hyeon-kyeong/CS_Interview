# 계수 정렬(Counting Sort)

### 계수 정렬이란?

특정 조건(원소가 정수이며 0 ~ K(K = 정수)의 범위안에 포함될 때)이 부합하면 배열 원소간 비교하지 않고 데이터가 몇번 등장했는지 세어 정렬을 진행하는 알고리즘

가장 큰 데이터의 크기로 배열을 선언하며 0 ~ K까지 모든 범위를 포함할 수 있어야함
### 과정

1. index K를 참조할 수 있는 K + 1크기의 countArr배열을 선언하고 모든 값을 0으로 초기화함

2. 원본 배열의 첫번째 index부터 원본 배열의 원소 값을 index로 가지는 countArr배열의 원소 값을 1씩 증가시킴\
   countArr[arr[i]]++;

3. 원본 배열의 마지막 index(K)까지 순회하고 나면 countArr 배열에 원본 배열 데이터들의 등장 횟수가 담기게 됨

4. countArr 배열의 index를 순회하며 index의 값이 0이 될 때까지 출력을 반복함

### 코드(Java)
```Java
int arr[5];  // [5, 4, 3, 2, 1]
int sorted_arr[5];
// 과정 1 - countArr 배열의 사이즈를 최대값 5가 담기도록 크게 잡음
int countArr[6];  // 단점 : countArr 배열의 사이즈의 범위를 가능한 값의 범위만큼 크게 잡아야 하므로 비효율적임

// 과정 2 - countArr 배열의 값을 증가해줌
for (int i = 0; i < arr.length; i++) {
    countArr[arr[i]]++;
}
// 과정 3 - countArr 배열을 누적합으로 만들어줌
for (int i = 1; i < countArr.length; i++) {
    countArr[i] += countArr[i - 1];
}
// 과정 4 - 뒤에서부터 배열을 돌면서, 해당하는 값의 인덱스에 값을 넣어줌
for (int i = arr.length - 1; i >= 0; i--) {
    countArr[arr[i]]--;
    sorted_arr[countArr[arr[i]]] = arr[i];
}
```

* 장점
  
  * 데이터간 비교를 진행하지 않아 O(n)이라는 시간 복잡도의 성능을 보여줌
  
  * 데이터 간 차이가 크지 않을 때 유리함
  
* 단점

  * 메모리 낭비가 심함\
    주어진 데이터가 (0, 1, 2, 10000)이라면 10000크기의 배열을 선언해야함
  
### 시간 복잡도

* O(n + k)

### 공간 복잡도

정렬을 수행할 데이터의 개수 n, 최댓값 k까지의 공간이 필요하므로 O(n + k)가 됨
