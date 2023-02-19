# 이분 탐색(Binary Search)

### 이분 탐색이란?

정렬된 수열에서 탐색 범위를 반으로 줄여 선형 탐색보다 훨씬 빠르게 탐색하는 방법

### 과정

1. 배열(arr)을 오름차순으로 정렬함

2. left와 right를 지정하고 mid(= (left + right) / 2)를 정함

3. arr[mid]가 찾는 값과 같다면 검색 종료

&nbsp;&nbsp;&nbsp;3-1. arr[mid]가 찾는 값보다 작다면 start를 mid + 1로 지정하고 2번 과정부터 다시 진행

&nbsp;&nbsp;&nbsp;3-2. arr[mid]가 찾는 값보다 크다면 end를 mid + 1로 지정하고 2번 과정부터 다시 진행

4. 값을 찾지 못했을 때 위의 과정을 start < end동안 계속해서 반복함

### 코드(Java)
```Java
public static int solution(int[] arr, int target) { // arr 배열에서 target을 찾음
	
    Arrays.sort(arr); // arr을 오름차순 정렬함
	
    int start = 0;
    int end = arr.length - 1;
    int mid = 0;

    while (start < end) {
        mid = (start + end) / 2;
        
        if (target == arr[mid]) {
            return mid;
        }
        else if (arr[mid] < target) {
            start = mid + 1;
        }
        else if (arr[mid] > target) {
            end = mid - 1;
        }
    }
}
```

* 장점
  
  * 탐색 범위를 반으로 줄이므로 선형 탐색(O(N))에 비해 매우 빠름
  
* 단점

  * 검색 원리 상 정렬이 가능한, 정렬된 배열에만 사용할 수 있음
  
### 시간 복잡도

* O(logN)
