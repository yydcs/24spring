# Assignment #F: All-Killed 满分

Updated 1844 GMT+8 May 20, 2024

2024 spring, Complied by ==崔灏梵 生命科学学院==



**说明：**

1）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

2）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

3）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：macOS Ventura 13.4.1 (c)

Python编程环境：Spyder IDE 5.2.2, PyCharm 2023.1.4 (Professional Edition)

C/C++编程环境：Mac terminal vi (version 9.0.1424), g++/gcc (Apple clang version 14.0.3, clang-1403.0.22.14.1)



## 1. 题目

### 22485: 升空的焰火，从侧面看

http://cs101.openjudge.cn/practice/22485/



思路：



代码

```python
# 
n=int(input())
fic={}
for i in range(n):
    fic[i+1]=list(map(int,input().split()))
stack=[(1,0)]
out=[]
height=-1
parent=1
while stack:
    node,h=stack.pop(0)
    if h>height:
        height=h
        out.append(parent)
    for j in fic[node]:
        if j!=-1:
            stack.append((j,h+1))
    parent=node
    if not stack:
        out.append(node)
del out[0]
s=' '.join(map(str,out))
print(s)
```



代码运行截图 ==（至少包含有"Accepted"）==

![841104cde2c15e6be6be97a8318c9ae](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\841104cde2c15e6be6be97a8318c9ae.png)



### 28203:【模板】单调栈

http://cs101.openjudge.cn/practice/28203/



思路：



代码

```python
# 
n=int(input())
dis=[0 for _ in range(n)]
nums=list(map(int,input().split()))
stack=[(nums[0],0)]
i=1
for i in range(n):
    while stack and nums[i]>stack[-1][0]:
        num,a=stack.pop()
        dis[a]=i+1
    stack.append((nums[i],i))
print(*dis)
```



代码运行截图 ==（至少包含有"Accepted"）==

![47991898a538470d6e81e177bf4ed5a](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\47991898a538470d6e81e177bf4ed5a.png)



### 09202: 舰队、海域出击！

http://cs101.openjudge.cn/practice/09202/



思路：



代码

```python
# 
from collections import defaultdict
def dfs(p):
    vis[p] = True
    for q in graph[p]:
        in_degree[q] -= 1
        if in_degree[q] == 0:
            dfs(q)
for _ in range(int(input())):
    n, m = map(int, input().split())
    graph = defaultdict(list)
    in_degree = [0] * (n + 1)
    vis = [False] * (n + 1) 
    for _ in range(m):
        x, y = map(int, input().split())
        graph[x].append(y)
        in_degree[y] += 1
    for k in range(1, n + 1):  
        if in_degree[k] == 0 and not vis[k]:  
            dfs(k)
    flag = any(not vis[i] for i in range(1, n + 1))  
    print('Yes' if flag else 'No')

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![62817050eea86fa64bfc43e0351f93c](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\62817050eea86fa64bfc43e0351f93c.png)



### 04135: 月度开销

http://cs101.openjudge.cn/practice/04135/



思路：



代码

```python
# 
n, m = map(int, input().split())
L = list(int(input()) for x in range(n))
def check(x):
    num, cut = 1, 0
    for i in range(n):
        if cut + L[i] > x:
            num += 1
            cut = L[i]
        else:
            cut += L[i]
    if num > m:
        return False
    else:
        return True
max_max = sum(L)
min_max = max(L)
while min_max < max_max:
    middle = (max_max + min_max) // 2
    if check(middle):
        max_max = middle
    else:
        min_max = middle + 1
print(max_max)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![591e67dcd66c2cb1affcc6b7c9444e9](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\591e67dcd66c2cb1affcc6b7c9444e9.png)



### 07735: 道路

http://cs101.openjudge.cn/practice/07735/



思路：



代码

```python
# 
import heapq

K, N, R = map(int, [input() for _ in range(3)])
graph = {i: [] for i in range(1, N+1)}
visited = {i: float('inf') for i in range(1, N+1)}
for _ in range(R):
    S, D, L, T = map(int, input().split())
    graph[S].append((D, L, T))

queue, ans = [(0, 0, 1)], -1
while queue:
    l, t, s = heapq.heappop(queue)
    if s == N:
        ans = l
        break
    visited[s] = t
    for d, z, w in graph[s]:
        if t+w < visited[d] and t+w <= K:
            heapq.heappush(queue, (l+z, t+w, d))
print(ans)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![c0ecc520eed0ba3eacf4aea6e3e5871](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\c0ecc520eed0ba3eacf4aea6e3e5871.png)



### 01182: 食物链

http://cs101.openjudge.cn/practice/01182/



思路：



代码

```python
# 
p=[0]*150001
def find(x):
    if p[x] == x:
        return x
    else:
        p[x] = find(p[x])
        return p[x]
n, k = map(int,input().split())
p=[0]*(3*n+1)
for i in range(3*n+1):
    p[i]=i
ans=0
for _ in range(k):
    a,x,y = map(int, input().split())
    if x >n or y >n:
        ans+=1
        continue
    if a==1:
        if find(x+n)==find(y) or find(y+n)==find(x):
            ans+=1
            continue
        p[find(x)]=find(y)
        p[find(x+n)] = find(y + n)
        p[find(x+2*n)] = find(y+2*n)
    else:
        if find(x) == find(y) or find(y + n) == find(x):
            ans += 1
            continue
        p[find(x + n)] = find(y)
        p[find(y + 2 * n)] = find(x)
        p[find(x + 2 * n)] = find(y + n)
print(ans)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![31b3140d4facc325b300b11d4639646](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\31b3140d4facc325b300b11d4639646.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

最后一题食物链，一直没有想到如何进行整类的合并，题解很巧妙



