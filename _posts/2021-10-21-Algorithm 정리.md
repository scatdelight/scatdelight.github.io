---
layout:     post
title:      "알고리즘 정리"
subtitle:   " \"Algorithm\""
date:       2021-10-20 12:00:00
author:     "Yongmin"
header-img: "img/gyul.jpg"
catalog: true
tags:
    - Algorithm
  
---

# 알고리즘

- ``에라토스테네스의 체 : 찾고자 하는 범위의 최대값의 제곱근까지 2, 3, 4씩 곱한 수들을 제거해나간다. (=배수는 소수가 아님) 제거되지 않은 수들은 소수이다.``

```python
import sys
import math

def isPrime(num):
    if num == 1:
        return False
    
    n = int(math.sqrt(num))

    for k in range(2, n+1):
        if num % k == 0: 
            return False
    
    return True 

m, n = map(int, input().split())

for i in range(m, n+1):
    if isPrime(i):
        print(i)
```


-  ``하노이의 탑 이동 순서 : 원판을 다른 곳으로 움직이는 함수를 hanoi라고 정의하면, n개의 원판 중 먼저 제일 큰 원판을 옮기기 위해선 그 위에 있는 n-1개의 원판을 이동시켜야 한다.(=hanoi(n-1))  
그 이후 제일 큰 원판을 움직이고(=hanoi(1)), n-1개의 원판을 그 위에 쌓는다.(=hanoi(n-1)) 그러므로, An+1 = 2*An + 1 이 된다. 이 것을 정리하면, n개의 원판을 다른 곳으로 옮기기 위한 이동 횟수의 점화식은 An = 2^n - 1이 된다.  
움직이는 방법은 n-1개를 재귀함수로 start -> to -> mid로 계속해서 움직여준다. 그 중에서 가장 큰 원판을 to로 옮겼을 때 그 해당 이동을 출력하고, 다시 n-1개의 원판을 mid -> start -> to로 이동시킨다.``

```python
n = int(input())
def hanoi(n, a, b, c):
    if n == 1:
        print(a, c)
    else:
        hanoi(n - 1, a, c, b)
        print(a, c)
        hanoi(n - 1, b, a, c)
print(2**n-1)
hanoi(n, 1, 2, 3)
```


- ``브루트 포스 : 모든 경우를 탐색하는 알고리즘으로, for 문을 여러개 사용하여 시간적으로 매우 불리하게 탐색하는 경우가 많은 알고리즘``


- ``백트래킹 : DFS기반 알고리즘으로, 한 경로를 따라 들어가다가 틀린 경우가 나왔을 경우 이전 상태로 돌아가서 다른 경로로 탐색하는 알고리즘``

```python
n,m = list(map(int,input().split()))
s = []
def dfs(start):
    if len(s)==m:
        print(' '.join(map(str,s)))
        return
    
    for i in range(start,n+1):
        if i not in s:
            s.append(i)
            dfs(i+1)
            s.pop()
dfs(1)
```


- ``동적 계획법(DP) : 배열을 통해 index마다의 특정 정보를 담고 이것을 활용하여 그 다음 index를 구해내는 알고리즘. ``

ex) LIS(Longest Increasing Subsequence, 가장 긴 증가하는 부분 수열) : 가장 긴 증가하는 부분 수열을 찾는 부분 수열을 찾는 문제로, 증가하는 값이 있을 때 그 전까지의 index에서 최대값에 +1을 하는 것을 반복

```python
x = int(input())

arr = list(map(int, input().split()))

dp = [1 for i in range(x)]

for i in range(x):
    for j in range(i):
        if arr[i] > arr[j]:
            dp[i] = max(dp[i], dp[j]+1)

print(max(dp))
```

ex) LCS(Longest Common Subsequence, 최장 공통 부분 수열) : 두 문자열을 공통 부분 수열 중에서 최장값을 찾는 문제로, 두 가지의 경우를 나눠서 dp를 적용한다.
dp[i][j] = 첫번째 문자열 i번째 문자와 두번째 문자열 j번째 문자까지 비교하였을 때 LCS 값
 1) 비교하고 있는 문자가 같다면 : dp 최대값 + 1
 2) 비교하교 있는 문자가 다르다면 : max(dp[i-1][j], dp[i][j-1])
를 적용한다.

```python
import sys

S1 = sys.stdin.readline().strip().upper()
S2 = sys.stdin.readline().strip().upper()
len1 = len(S1)
len2 = len(S2)
matrix = [[0] * (len2 + 1) for _ in range(len1 + 1)]

for i in range(1, len1 + 1):
    for j in range(1, len2 + 1):
        if S1[i - 1] == S2[j - 1]:
            matrix[i][j] = matrix[i - 1][j - 1] + 1
        else:
            matrix[i][j] = max(matrix[i - 1][j], matrix[i][j - 1])

print(matrix[-1][-1])
```
