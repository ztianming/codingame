# ROBBERY OPTIMISATION
## Goal
Rob is a robber. He wants to operate a last time in the neighborhood before he leaves.
He has been informed about the values of the content of each house of a street but he is careful and when he robs in a house he avoids the 2 houses aside (left and right).
What is the maximum money he can make without being caught?
! Be warned ! Some houses have been trapped. They have been rated with negative values.

For example, for a street of 3 houses with values: (A: 1) - (B: 2) - (C: 3), Rob shall visit houses A and C (he takes 4).
In this other street: (A: 1) - (B: 15) - (C: 10) - (D: 13) - (E: 16), Rob should avoid C and D and visit only B and E (he takes 31).  
Input  
Line 1: An integer N for the number of houses in the street.  
Next N lines: The value housevalue of the nth house content.  
Output  
Line 1: A single integer being the maximum amount Rob can make in the street.  
Constraints  
1 ≤ N ≤ 100  
housevalue < 10^13  
Example  
Input  
5  
1  
15  
10  
13  
16  
Output  
31  

## solution

### python
```python
import sys
import math

# 0 2 3 or 1 3 4
# 2 4 5 or 3 5 6 or 3 5 6 or 4 6 7

def calc(index):
    if index >= n:
        return 0
    
    if maxmum[index] != 0:
        return maxmum[index]
    
    max_right = max(calc(index+2), calc(index+3))

    maxmum[index] = (houses[index] if houses[index] >0 else 0) +(max_right if max_right>0 else 0)
    # 
    return maxmum[index]


n = int(input())
houses=[0]*n
maxmum = [0]*n
for i in range(n):
    houses[i] = int(input())

print(houses, file=sys.stderr)

res = max(calc(0), calc(1))
print(maxmum, file=sys.stderr)
print(res)

```

```python
# 评分最高的解法
from functools import lru_cache
# 最近最少使用缓存装饰器
# 根据参数缓存每次函数调用结果，对于相同参数的，无需重新函数计算，直接返回之前缓存的返回值；
@lru_cache()
def rec(i=0):
    if i >= len(street): return 0
    return max(rec(i+1), street[i]+rec(i+2))

street = [int(input()) for _ in range(int(input()))]
print(rec())
```
## Goal
n clones of Fokz are standing in a circular order (numbered from 1 to n) . Number 1 has a sword. He kills the next person (i.e. No. 2) and gives the sword to the next (i.e. No. 3). All people do the same until only 1 survives. You are expected to output the number of the last survivor.
{Where should the real Fokz stand so that he is the last survivor?}  
Input  
1 Line containing a number n  
Output  
Number of the last survivor  
Constraints  
1 <= n <= 10^5  
Example  
Input  
5  
Output  
3  
### Solution
约瑟夫环
```python
def josephus(n, k):
    # n代表总人数，k代表报数的数字
    List = list(range(1, n + 1))
    index = 0
    while List:
        temp = List.pop(0)
        index += 1
        if index == k:
            index = 0
            continue
        List.append(temp)
        if len(List) == 2:
            print(List[-1])
            break
print(j(n, 2))
```
```python
def j(n,k):
    r=0
    for i in range(1, n+1):
        r=(r+k)%i
    return r+1
n = int(input())
print(j(n, 2))
```
