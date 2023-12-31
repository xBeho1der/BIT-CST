# 扔水杯问题项目详解
## 目标
- 给你 k 个相同的水杯，并可以使用一栋从第 1 层到第 n 层共有 n 层楼的高层建筑。

- 已知存在楼层 f ，满足 0 <= f <= n ，任何从 高于 f 的楼层落下的水杯都会碎，从 f 楼层或比它低的楼层落下的水杯都不会破。

- 每次你可以拿一个没有碎的水杯并把它从任一楼层 x 扔下（满足 1 <= x <= n）。如果水杯碎了，你就不能再次使用它。如果某个水杯扔下后没有摔碎，则可以在之后的操作中重复使用这个水杯。

- 请你计算并返回要确定 f 确切的值的最小操作次数是多少？

## 操作
### 动态规划
- 不难想到，在第x层扔下水杯时，如果水杯破碎，则变为k-1个水杯，x-1层的扔水杯问题；若水杯不破碎，则变为k个水杯，n-x层的子问题，但是该算法递归次数过多，运行时间较长，时间复杂度为o(kn^2)
### 状态转移条件下的逆向思维
- 根据题目条件，不难发现，原题目等价于在能做i次操作的条件下，通过k个水杯找到能找到的最高层n，因此可以假设函数f(i,k)，i代表操作次数，k代表水杯数量，满足```f(i,k) = 1+f(i-1,k-1)+f(i-1,k)```
- 对于等式可以理解为：如果水杯碎了，则这一层的下方可以有f(i-1,k-1)层；如果没碎，则本层的上方有f(i-1,k)层，同时再加上本层层数1，即为上等式
- 在k=1时，f=i；i=1时，f=1
- 在最坏的情况下，i取值不会超过n，因此只需0<=i<=n遍历求出所有的f(i,k)即可

## 实现
```python
def cup_drop(k: int, n: int) -> int:
    '''
    solution to this question
    :type k: int
    :type n: int
    '''
    if n == 1:
        return 1
    f = [[0]*(k+1) for _ in range(n+1)]
    for i in range(1, k+1):
        f[1][i] = 1
    res = -1
    for i in range(2, n+1):
        for j in range(1, k+1):
            f[i][j] = 1+f[i-1][j-1]+f[i-1][j]
        if f[i][j] >= n:
            res = i
            break
    return res
```