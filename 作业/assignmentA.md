# Assignment #A: 图论：遍历，树算及栈

Updated 2018 GMT+8 Apr 21, 2024

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

### 20743: 整人的提词本

http://cs101.openjudge.cn/practice/20743/



思路：



代码

```python
# 
i=0
ss=input()
s=[]
for j in ss:
    s.append(j)
stack=[]
while i <len(s):
    if s[i]=='(':
        stack.append(i)
        s.pop(i)
    elif s[i]==')':
        s.pop(i)
        le=stack.pop()
        tis=s[le:i]
        ti=[]
        for j in range(1,len(tis)+1):
            ti.append(tis[-j])
        s=s[:le]+ti+s[i:]
    else:
        i+=1
print(''.join(s))
```



代码运行截图 ==（至少包含有"Accepted"）==

![9fecfee8346b572c5e9803ded58e97c](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\9fecfee8346b572c5e9803ded58e97c.png)



### 02255: 重建二叉树

http://cs101.openjudge.cn/practice/02255/



思路：



代码

```python
# 
class Treenode:
    def __init__(self,val):
        self.val=val
        self.left=None
        self.right=None

def build_tree(pre,ino):
    root=Treenode(pre[0])
    node=pre[0]
    a=ino.index(node)
    pre1=pre[1:a+1]
    pre2=pre[a+1:]
    ino1=ino[:a]
    ino2=ino[a+1:]
    if pre1:
        root.left=build_tree(pre1,ino1)
    if pre2:
        root.right=build_tree(pre2,ino2)
    return root

def postorder(root):
    output=[]
    if root.left:
        output.extend(postorder(root.left))
    if root.right:
        output.extend(postorder(root.right))
    output.append(root.val)
    return output

while True:
    try:
        nu=input().split()
        root=build_tree(nu[0],nu[1])
        print(''.join(postorder(root)))
    except EOFError:
        break
```



代码运行截图 ==（至少包含有"Accepted"）==

![63487456e5a37920a245696117f6624](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\63487456e5a37920a245696117f6624.png)



### 01426: Find The Multiple

http://cs101.openjudge.cn/practice/01426/

要求用bfs实现



思路：



代码

```python
# 
def bei(n):
    s=1
    i=bin(s)[2:]
    while int(i)%n!=0:
        s+=1
        i=bin(s)[2:]
    return int(i)
while True:
    s=input()
    if s=='0':
        break
    else:
        print(bei(int(s)))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![63487456e5a37920a245696117f6624](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\63487456e5a37920a245696117f6624.png)



### 04115: 鸣人和佐助

bfs, http://cs101.openjudge.cn/practice/04115/



思路：



代码

```python
# 
from collections import deque

dire = [(-1, 0), (0, -1), (1, 0), (0, 1)]
flag = 0
ans = 0

def bfs(x, y, t):
    visited = set()
    global ans, flag
    q = deque()
    q.append((t, x, y, 0))
    while q:
        t, x, y, ans = q.popleft()
        for dx, dy in dire:
            nx = x + dx
            ny = y + dy
            if 0 <= nx < m and 0 <= ny < n:
                if g[nx][ny] != "#":
                    nt = t
                else:
                    nt = t - 1
                if nt >= 0 and (nt, nx, ny) not in visited:
                    newans = ans + 1
                    if g[nx][ny] == "+":
                        flag = 1
                        return flag, newans
                    q.append((nt, nx, ny, newans))
                    visited.add((nt, nx, ny))
    return flag, ans

m, n, t = map(int, input().split())
g = []
for i in range(m):
    g.append(list(input()))
for i in range(m):
    for j in range(n):
        if g[i][j] == "@":
            x = i
            y = j
flag, newans = bfs(x, y, t)
if flag:
    print(newans)
else:
    print(-1)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![6042f98f61685d54bc0790fc279ab61](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\6042f98f61685d54bc0790fc279ab61.png)



### 20106: 走山路

Dijkstra, http://cs101.openjudge.cn/practice/20106/



思路：



代码

```python
# 
from heapq import heappop, heappush

def bfs(x1, y1):
    q = [(0, x1, y1)]
    v = set()
    while q:
        t, x, y = heappop(q)
        v.add((x, y))
        if x == x2 and y == y2:
            return t
        for dx, dy in dir:
            nx, ny = x+dx, y+dy
            if 0 <= nx < m and 0 <= ny < n and ma[nx][ny] != '#' and (nx, ny) not in v:
                nt = t+abs(int(ma[nx][ny])-int(ma[x][y]))
                heappush(q, (nt, nx, ny))
    return 'NO'


m, n, p = map(int, input().split())
ma = [list(input().split()) for _ in range(m)]
dir = [(1, 0), (-1, 0), (0, 1), (0, -1)]
for _ in range(p):
    x1, y1, x2, y2 = map(int, input().split())
    if ma[x1][y1] == '#' or ma[x2][y2] == '#':
        print('NO')
        continue
    print(bfs(x1, y1))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![c4540710afc52b050961c031ef748e7](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\c4540710afc52b050961c031ef748e7.png)



### 05442: 兔子与星空

Prim, http://cs101.openjudge.cn/practice/05442/



思路：



代码

```python
# 
class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.rank = [0] * n
    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]
    def union(self, x, y):
        root_x = self.find(x)
        root_y = self.find(y)
        if root_x != root_y:
            if self.rank[root_x] < self.rank[root_y]:
                self.parent[root_x] = root_y
            elif self.rank[root_x] > self.rank[root_y]:
                self.parent[root_y] = root_x
            else:
                self.parent[root_y] = root_x
                self.rank[root_x] += 1
def calculate_minimum_weight(n, edges):
    sorted_edges = sorted(edges, key=lambda x: x[2])
    total_weight = 0
    count = 0
    union_find = UnionFind(n)
    for edge in sorted_edges:
        src, dest, weight = edge
        root_src = union_find.find(ord(src) - 65)
        root_dest = union_find.find(ord(dest) - 65)
        if root_src != root_dest:
            total_weight += weight
            count += 1
            union_find.union(root_src, root_dest)
            if count == n - 1:
                break
    return total_weight
n = int(input())
edges = []
for _ in range(n - 1):
    line = input().split()
    src = line[0]
    num_edges = int(line[1])
    for i in range(2, 2 + num_edges * 2, 2):
        dest = line[i]
        weight = int(line[i + 1])
        edges.append((src, dest, weight))

minimum_weight = calculate_minimum_weight(n, edges)
print(minimum_weight)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![0ae3f69d19209d12f59ba0da7d0c5a5](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\0ae3f69d19209d12f59ba0da7d0c5a5.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

之前计概没有学过bfs,dfs略微吃力，但是做题逐渐熟悉



