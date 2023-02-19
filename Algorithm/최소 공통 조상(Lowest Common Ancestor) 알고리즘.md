# 최소 공통 조상(Lowest Common Ancestor) 알고리즘

### 최소 공통 조상 알고리즘이란?

두 정점이 만나는 최초 부모 정점(최소 공통 조상)을 찾는 알고리즘

<img width="40%" src="https://user-images.githubusercontent.com/75103526/208243947-1e8f6046-fbc8-4206-b66a-2eb69374214d.png"/>

LCA(2, 5) = 1  2와 5의 첫 부모 정점은 1\
LCA(4, 7) = 1  7과 4의 첫 부모 정점은 1\
LCA(6, 9) = 5  9와 6의 첫 부모 정점은 5

### 과정

1. 1번 루트 노드를 기준으로 DFS 탐색을 통해 각 노드의 트리 높이(depth)와 부모 노드(parent)를 저장함

2. LCA를 구하기 위한 a, b노드가 주어졌을 때 두 노드의 dpeth를 동일하게 맞춤 (depth[a] = depth[b])

3. 각 노드의 부모 노드가 일치할 때까지 비교를 반복함 (parent[a] = parent[b])

### 코드(Java)
```Java
void LCA(int[] depth, int[] parent, int a, int b)
{
   int aDepth = depth[a];
   int bDepth = depth[b];
   
   while (aDepth > bDepth) {
     a = parent[a];
     aDepth--;
   }
   
   while (aDetph < bDepth) {
     b = parent[a];
     bDepth--;
   }
   
   while (a != b) {
     a = parent[a];
     b = parent[b];
   }
   
   return a;
}
```

### 시간 복잡도

* DP 사용 : O(NlongN + MlongN)
* 세그먼트 트리 사용 : (N + MlongN)
