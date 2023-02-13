# 퀵 정렬(Quick Sort)

### 퀵 정렬이란?

퀵 정렬은 분할 정복(divide and conquer)을 활용하는 정렬로 리스트 중 하나를 pivot으로 정하고 pivot을 기준으로 작은 수는 왼쪽, 큰 수는 오른쪽으로 옮기는 작업을 재귀적으로 반복하여 정렬을 수행함

    분할 정복(divide and conquer)
    
    엄청나게 크고 방대한 문제를 조금씩 조금씩 나눠가면서 용이하게 풀 수 있는 문제 단위로 나눈 다음 그것들을 다시 합쳐서 해결하는 개념
    
    분할: 문제를 더이상 분할할 수 없을 때까지 동일한 유형의 여러 하위 문제로 나눔
    정복: 가장 작은 단위의 하위 문제를 해결하여 정복함
    조합: 하위 문제에 대한 결과를 원래 문제에 대한 결과로 조합함
    

### 과정

1. 배열 중 하나의 원소를 pivot으로 정함

2. pivot 앞(왼쪽)에는 pivot보다 작은 원소가, 뒤(오른)쪽에는 pivot보다 큰 원소가 오도록 배열을 나눔 : 분할(divide)

3. 분할된 두 배열에 대해 1, 2과정을 재귀를 통해 반복함

(재귀 호출 시, 최소 하나의 원소는 최종 위치가 정해지므로 해당 알고리즘의 종료를 항상 보장할 수 있음)

### 코드(Java)

* 정복(conquer)

  부분 배열을 정렬하는 역할을 하며 부분 배열의 크기가 충분히 작지 않으면 순환 호출을 통해 다시 분할 정복을 진행함
  
```Java
public void quickSort(int[] array, int left, int right) {
    if(left >= right) return;
    
    // 분할 
    int pivot = partition(); 
    
    // 피벗은 제외한 2개의 부분 배열을 대상으로 순환 호출
    quickSort(array, left, pivot-1);  // 정복(Conquer)
    quickSort(array, pivot+1, right); // 정복(Conquer)
}
```

* 분할(divide)

  pivot을 중심으로 왼쪽에는 pivot보다 작은 값, 오른쪽에는 pivot보다 큰 값으로 나눠 2개의 부분 배열을 만듦

```Java
public int partition(int[] array, int left, int right) {
    /**
    // 최악의 경우, 개선 방법
    int mid = (left + right) / 2;
    swap(array, left, mid);
    */
    
    int pivot = array[left]; // 가장 왼쪽값을 피벗으로 설정
    int i = left, j = right;
    
    while(i < j) {
        while(pivot < array[j]) {
            j--;
        }
        while(i < j && pivot >= array[i]){
            i++;
        }
        swap(array, i, j);
    }
    array[left] = array[i];
    array[i] = pivot;
    
    return i;
}
```

* 장점
  
  * 불필요한 데이터의 이동을 줄이고 먼거리의 데이터를 교환함\
    한 번 결정된 pivot은 추후 연산에서 제외됨\
    => O(nlog₂n)의 시간 복잡도를 가지는 알고리즘 중에서 가장 빠른 알고리즘임
    
  * 정렬하고자 하는 배열 내에서 교환을 진행하는 형태로, 별도의 메모리 공간을 필요로하지 않는 제자리 정렬(in-place sorting)임
  
* 단점

  * <b>불안정 정렬(Unstable Sort)</b>임
  * 이미 정렬된 배열에서 퀵소트를 수행할 경우 불균형 분할이 발생해 수행시간이 더 오래걸림
  
### 시간 복잡도

* 최선 : O(nlog₂n)
* 평균 : O(nlog₂n)
* 최악 : O(n^2)

### 공간 복잡도

주어진 배열 안에서 교환(swap)을 통해 정렬이 수행되므로 <b>O(n)</b>임
