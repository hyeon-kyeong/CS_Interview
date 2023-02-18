# 병합 정렬(Merge Sort)

퀵 정렬, 힙 정렬과 마찬가지로 평균 Θ(nlogn)의 시간 소요

분할 정복 방법을 통해 구현

퀵정렬과의 차이점
> 퀵정렬 : 우선 피벗을 통해 정렬(partition) → 영역을 쪼갬(quickSort)  
> 합병정렬 : 영역을 쪼갤 수 있을 만큼 쪼갬(mergeSort) → 정렬(merge)

```
mergeSort(A[], p, r)
{
    if (p < r) then {
        q ← [(p+r)/2]
        mergeSort(A, p, q)
        mergeSort(A, q+1, r)
        merge(A,p,q,r)
    }
}

merge(A[], p, q, r)
{
    정렬되어 있는 두 배열 A[p...q]와 A[q+1...r]을 합쳐
    정렬된 하나의 배열 A[p...r]을 만든다
}
```

Java Code

```java
public void mergeSort(int[] array, int left, int right) {
    
    if(left < right) {
        int mid = (left + right) / 2;
        
        mergeSort(array, left, mid);
        mergeSort(array, mid+1, right);
        merge(array, left, mid, right);
    }
    
}

public static void merge(int[] array, int left, int mid, int right) {
    int[] L = Arrays.copyOfRange(array, left, mid + 1);
    int[] R = Arrays.copyOfRange(array, mid + 1, right + 1);
    
    int i = 0, j = 0, k = left;
    int ll = L.length, rl = R.length;
    
    while(i < ll && j < rl) {
        if(L[i] <= R[j]) {
            array[k] = L[i++];
        }
        else {
            array[k] = R[j++];
        }
        k++;
    }
    
    // remain
    while(i < ll) {
        array[k++] = L[i++];
    }
    while(j < rl) {
        array[k++] = R[j++];
    }
}
```

## 시간복잡도

**최선**: Ω(nlogn)

**평균**: Θ(nlogn)	

**최악**: O(nlogn)
	

## 공간복잡도

O(n)

## 장점

- 안정 정렬
- 데이터의 분포에 영향을 덜 받음


## 단점

- 임시 배열이 필요함

- 만약 레코드들의 크기가 큰 경우 이동 횟수가 많으므로 매우 큰 시간적 낭비를 초래함

그러나 , 만약 레코드를 연결 리스트로 구성하여 합병 정렬할 경우, 링크 인덱스만 변경되므로 데이터의 이동은 무시할 수 있을 정도로 작아짐. 

따라서, 크기가 큰 레코드를 정렬할 경우, 만약 연결 리스트를 사용한다면, 합병 정렬은 퀵 정렬을 포함한 다른 어떤 정렬 방법보다 효율적일 수 있음. 