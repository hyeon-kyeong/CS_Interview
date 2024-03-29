# 삽입 정렬(Insertion Sort)

### 삽입 정렬이란?

삽입 정렬은 자료 배열의 모든 요소를 앞에서부터 이미 차례대로 정렬된 배열 부분과 비교하여 자신의 위치에 삽입하는 정렬임

### 과정

1. 두번째에 위치한 값을 target에 저장함

2. target과 target 앞에 있는 원소들을 비교하여 원소들을 뒤로 옮기고 target을 삽입합 위치를 정함

3. 지정된 자리에 target을 삽입함

4. 1번으로 돌아가 다음 위치의 값을 target에 저장하고 과정을 반복함

### 코드(Java)
```Java
void insertionSort(int[] arr)
{
   for(int i = 1; i < arr.length; i++){
      int target = arr[i];
      int j = i - 1;
      while((j >= 0) && (arr[j] > target)) {
         arr[j + 1] = arr[j];
         j--;
      }
      arr[j + 1] = target;
   }
}
```

* 장점
  
  * 알고리즘 자체가 단순하며 <b>안정 정렬(Stable Sort)</b>임
  
  * 원소가 이미 정렬되어 있는 경우 매우 효율적임
  
  * 정렬하고자 하는 배열 내에서 교환을 진행하는 형태로, 별도의 메모리 공간을 필요로하지 않는 제자리 정렬(in-place sorting)임
  
  * 버블 정렬이나 선택 정렬과 동일한 시간 복잡도(O(n^2))를 보여주지만 상대적으로 빠름
  
* 단점

  * 평균과 최악의 시간 복잡도가 O(n^2)으로 비효율적임
  
  * 버블 정렬과 선택 정렬과 마찬가지로 배열의 길이가 길수록 비효율적임(비교적 많은 배열 값들을 이동하기 때문)
  
### 시간 복잡도

* 최선 : O(n)
* 평균 : O(n^2)
* 최악 : O(n^2)

### 공간 복잡도

주어진 배열 안에서 교환(swap)을 통해 정렬이 수행되므로 <b>O(n)</b>임
