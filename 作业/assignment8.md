# Assignment #8: 图论：概念、遍历，及 树算

Updated 1919 GMT+8 Apr 8, 2024

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

### 19943: 图的拉普拉斯矩阵

matrices, http://cs101.openjudge.cn/practice/19943/

请定义Vertex类，Graph类，然后实现



思路：



代码

```python
# 
n,m=map(int,input().split())
d=[[0 for i in range(n)] for j in range(n)]
a=[[0 for i in range(n)] for j in range(n)]
r=[]
for i in range(m):
    c,b=map(int,input().split())
    d[c][c]+=1
    d[b][b]+=1
    r.append((c,b))
for i in range(n):
    for j in range(n):
        if (i,j) in r or (j,i) in r:
            a[i][j]=1
            a[j][i]=1
for i in range(n):
    for j in range(n):
        d[i][j]-=a[i][j]
for i in range(n):
    print(' '.join(map(str,d[i])))
```



代码运行截图 ==（至少包含有"Accepted"）==

![b9adb73ee0602500e53f11beaaf2254](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\b9adb73ee0602500e53f11beaaf2254.png)



### 18160: 最大连通域面积

matrix/dfs similar, http://cs101.openjudge.cn/practice/18160



思路：



代码

```python
# 
dire = [[-1,-1],[-1,0],[-1,1],[0,-1],[0,1],[1,-1],[1,0],[1,1]]

area = 0
def dfs(x,y):
    global area
    if matrix[x][y] == '.':return
    matrix[x][y] = '.'
    area += 1
    for i in range(len(dire)):
        dfs(x+dire[i][0], y+dire[i][1])


for _ in range(int(input())):
    n,m = map(int,input().split())

    matrix = [['.' for _ in range(m+2)] for _ in range(n+2)]
    for i in range(1,n+1):
        matrix[i][1:-1] = input()

    sur = 0
    for i in range(1, n+1):
        for j in range(1, m+1):
            if matrix[i][j] == 'W':
                area = 0 
                dfs(i, j)
                sur = max(sur, area)
    print(sur)
```



代码运行截图 ==（至少包含有"Accepted"）==

![b05c635565bd24d3f65a966c49cd664](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\b05c635565bd24d3f65a966c49cd664.png)



### sy383: 最大权值连通块

https://sunnywhy.com/sfbj/10/3/383



思路：



代码

```python
# 
def max_weight(n,m,weights,edges):
    graph = [[] for _ in range(n)]
    for u, v in edges:
        graph[u].append(v)
        graph[v].append(u)
    visited = [False] * n
    max_weight = 0

    def dfs(node):
        visited[node] = True
        total_weight = weights[node]
        for neighbor in graph[node]:
            if not visited[neighbor]:
                total_weight += dfs(neighbor)
        return total_weight
    for i in range(n):
        if not visited[i]:
            max_weight = max(max_weight, dfs(i))
    return max_weight
n, m = map(int, input().split())
weights = list(map(int, input().split()))
edges = []
for _ in range(m):
    u, v = map(int, input().split())
    edges.append((u, v))
print(max_weight(n, m, weights, edges))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![04dd7aaec11571e0f3466882f2d2913](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\04dd7aaec11571e0f3466882f2d2913.png)



### 03441: 4 Values whose Sum is 0

data structure/binary search, http://cs101.openjudge.cn/practice/03441



思路：



代码

```python
# 
n = int(input())
a = [0]*(n+1)
b = [0]*(n+1)
c = [0]*(n+1)
d = [0]*(n+1)

for i in range(n):
    a[i],b[i],c[i],d[i] = map(int, input().split())

dict1 = {}
for i in range(n):
    for j in range(n):
        if not a[i]+b[j] in dict1:
            dict1[a[i] + b[j]] = 0
        dict1[a[i] + b[j]] += 1

ans = 0
for i in range(n):
    for j in range(n):
        if -(c[i]+d[j]) in dict1:
            ans += dict1[-(c[i]+d[j])]

print(ans)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![baada84db13cd61abd3af6bc145b71e](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\baada84db13cd61abd3af6bc145b71e.png)



### 04089: 电话号码

trie, http://cs101.openjudge.cn/practice/04089/

Trie 数据结构可能需要自学下。



思路：



代码

```python
# 
class TrieNode:
    def __init__(self):
        self.child={}


class Trie:
    def __init__(self):
        self.root = TrieNode()

    def insert(self, nums):
        curnode = self.root
        for x in nums:
            if x not in curnode.child:
                curnode.child[x] = TrieNode()
            curnode=curnode.child[x]

    def search(self, num):
        curnode = self.root
        for x in num:
            if x not in curnode.child:
                return 0
            curnode = curnode.child[x]
        return 1


t = int(input())
p = []
for _ in range(t):
    n = int(input())
    nums = []
    for _ in range(n):
        nums.append(str(input()))
    nums.sort(reverse=True)
    s = 0
    trie = Trie()
    for num in nums:
        s += trie.search(num)
        trie.insert(num)
    if s > 0:
        print('NO')
    else:
        print('YES')
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![872ef19fc4d4d942f094705f543537c](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\872ef19fc4d4d942f094705f543537c.png)



### 04082: 树的镜面映射

http://cs101.openjudge.cn/practice/04082/



思路：



代码

```python
# 
from collections import deque

class TreeNode:
    def __init__(self, x):
        self.x = x
        self.children = []

def create_node():
    return TreeNode('')

def build_tree(tempList, index):
    node = create_node()
    node.x = tempList[index][0]
    if tempList[index][1] == '0':
        index += 1
        child, index = build_tree(tempList, index)
        node.children.append(child)
        index += 1
        child, index = build_tree(tempList, index)
        node.children.append(child)
    return node, index

def print_tree(p):
    Q = deque()
    s = deque()
    while p is not None:
        if p.x != '$':
            s.append(p)
        p = p.children[1] if len(p.children) > 1 else None
    while s:
        Q.append(s.pop())
    while Q:
        p = Q.popleft()
        print(p.x, end=' ')
        if p.children:
            p = p.children[0]
            while p is not None:
                if p.x != '$':
                    s.append(p)
                p = p.children[1] if len(p.children) > 1 else None
            while s:
                Q.append(s.pop())


n = int(input())
tempList = input().split()
root, _ = build_tree(tempList, 0)
print_tree(root)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![d301693eb7f4cf343393d16f7139af8](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\d301693eb7f4cf343393d16f7139af8.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

这周期中寄，没有花足够的时间在数算上，又得找时间恶补了。



