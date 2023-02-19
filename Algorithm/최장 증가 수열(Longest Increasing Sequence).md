# 최장 증가 수열(Longest Increasing Sequence)


> 가장 긴 증가하는 부분 수열

[ 7, 2, 3, 8, 4, 5 ] → 해당 배열에서는 `[2, 3, 4, 5]`가 LIS로, 답은 `4`


## 구현 방법

- **DP**: O(n^2)
- **Lower Bound**: O(nlogn)


## DP 활용 코드

```java
int arr[] = {7, 2, 3, 8, 4, 5};
int dp[] = new int[arr.length]; // LIS 저장 배열


for(int i = 1; i < dp.length; i++) {
    for(int j = i-1; j>=0; j--) {
        if(arr[i] > arr[j]) {
            dp[i] = (dp[i] < dp[j]+1) ? dp[j]+1 : dp[i];
        }
    }
}

for (int i = 0; i < dp.length; i++) {
	if(max < dp[i]) max = dp[i];
}

// 저장된 dp 배열 값 : [0, 0, 1, 2, 2, 3]
// LIS : dp배열에 저장된 값 중 최대 값 + 1
```

배열의 크기가 커서 n^2로 해결할 수 없는 경우 Lower Bound를 활용하여 LIS를 구현해야 함


