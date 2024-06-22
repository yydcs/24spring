# Assignment #B: 图论和树算

Updated 1709 GMT+8 Apr 28, 2024

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

### 28170: 算鹰

dfs, http://cs101.openjudge.cn/practice/28170/



思路：



代码

```python
# 
def count_hawks(board):
    hawks = 0
    visited = set()
    def explore_hawk(row, col):
        if (row, col) in visited or board[row][col] != '.':
            return
        visited.add((row, col))
        for dr, dc in [(0, 1), (1, 0), (0, -1), (-1, 0)]:
            new_row, new_col = row + dr, col + dc
            if 0 <= new_row < 10 and 0 <= new_col < 10:
                explore_hawk(new_row, new_col)
    for row in range(10):
        for col in range(10):
            if board[row][col] == '.' and (row, col) not in visited:
                hawks += 1
                explore_hawk(row, col)
    return hawks
board = [list(input()) for _ in range(10)]
hawks = count_hawks(board)
print(hawks)
```



代码运行截图 ==（至少包含有"Accepted"）==

![3dc67ef0cce8a554bad63844479b714](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\3dc67ef0cce8a554bad63844479b714.png)



### 02754: 八皇后

dfs, http://cs101.openjudge.cn/practice/02754/



思路：



代码

```python
# 
def is_valid(s,x):
    y=len(s)+1
    if str(x) in s:
        return False
    else:
        for i in range(len(s)):
            if abs(y-i-1)==abs(x-int(s[i])):
                return False
    return True

def put(s):
    output=[]
    for i in range(1,9):
        if is_valid(s,i):
            output.append(s+str(i))
    return output

def thr(d):
    output=[]
    for i in d:
        if len(i)==8:
            return d
        else:
            dis=put(i)
            output.extend(dis)
    return thr(output)

record=[]
for i in range(1,9):
    record.append(str(i))
dis=thr(record)
dis=list(map(int,dis))
dis.sort()
t=int(input())
for i in range(t):
    b=int(input())
    print(dis[b-1])
```



代码运行截图 ==（至少包含有"Accepted"）==

![7ecfde528197fa8f25324413d57f52f](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\7ecfde528197fa8f25324413d57f52f.png)



### 03151: Pots

bfs, http://cs101.openjudge.cn/practice/03151/



思路：



代码

```python
# 
def solve(A, B, C):
    start=(0,0)
    visited=set()
    visited.add(start)
    queue=[(start, [])]
    while queue:
        (a,b), actions=queue.pop(0)
        if a == C or b == C:
            return actions
        next_states = [(A,b),(a,B),(0,b),(a,0),(min(a+b,A), max(0,a+b-A)),(max(0,a+b-B), min(a+b,B))]
        for i in next_states:
            if i not in visited:
                visited.add(i)
                new_actions = actions +[get_action(a,b,i)]
                queue.append((i, new_actions))
    return ["impossible"]
def get_action(a,b,next_state):
    if next_state ==(A,b):
        return "FILL(1)"
    elif next_state ==(a,B):
        return "FILL(2)"
    elif next_state ==(0,b):
        return "DROP(1)"
    elif next_state==(a,0):
        return "DROP(2)"
    elif next_state ==(min(a+b,A), max(0,a+b-A)):
        return "POUR(2,1)"
    else:
        return "POUR(1,2)"
A,B,C=map(int, input().split())
solution=solve(A, B, C)
if solution==["impossible"]:
    print(solution[0])
else:
    print(len(solution))
    for i in solution:
        print(i)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![b9c81c58aacc8353d699e225206e241](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\b9c81c58aacc8353d699e225206e241.png)



### 05907: 二叉树的操作

http://cs101.openjudge.cn/practice/05907/



思路：



代码

```python
# 
for i in range(int(input())):
    n, m = map(int, input().split())
    dic = {i: [0, 0, 0] for i in range(n)}
    for i in range(n):
        x, y, z = map(int, input().split())
        dic[x][1], dic[x][2] = y, z
        if y != -1:
            dic[y][0] = x
        if z != -1:
            dic[z][0] = x
    for j in range(m):
        s = list(map(int, input().split()))
        if s[0] == 1:
            x, y = s[1], s[2]
            x_father, y_father = dic[x][0], dic[y][0]
            x_idx, y_idx = 1 + (dic[x_father][2] == x), 1 + (dic[y_father][2] == y)
            dic[x_father][x_idx], dic[y_father][y_idx], dic[x][0], dic[y][0] = y, x, y_father, x_father
        else:
            x = s[1]
            while dic[x][1] != -1:
                x = dic[x][1]
            print(x)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![34940457248674933fca34f5b400fd3](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\34940457248674933fca34f5b400fd3.png)





### 18250: 冰阔落 I

Disjoint set, http://cs101.openjudge.cn/practice/18250/



思路：



代码

```python
# 
while True:
    try:
        n,m=map(int,input().split())
        dis={}
        cups=[]
        for i in range(1,n+1):
            dis[i]=i
            cups.append([i])
        for i in range(m):
            x,y=map(int,input().split())
            if dis[x] == dis[y]:
                print('Yes')
            else:
                a=dis[y]-1
                for j in cups[dis[y]-1]:
                    dis[j]=dis[x]
                cups[dis[x]-1]+=cups[a]
                cups[a]=[]
                print('No')
        out=[]
        for i in range(n):
            if cups[i]:
                out.append(str(i+1))
        print(len(out))
        print(' '.join(out))
    except Exception as e:
        break
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![212e8a766f910e09dcf4dc2c9442317](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\212e8a766f910e09dcf4dc2c9442317.png)



### 05443: 兔子与樱花

http://cs101.openjudge.cn/practice/05443/



思路：



代码

```python
# 
import heapq

def dijkstra(adjacency, start):
    distances = {vertex: float('infinity') for vertex in adjacency}
    previous = {vertex: None for vertex in adjacency}
    distances[start] = 0
    pq = [(0, start)]

    while pq:
        current_distance, current_vertex = heapq.heappop(pq)
        if current_distance > distances[current_vertex]:
            continue

        for neighbor, weight in adjacency[current_vertex].items():
            distance = current_distance + weight
            if distance < distances[neighbor]:
                distances[neighbor] = distance
                previous[neighbor] = current_vertex
                heapq.heappush(pq, (distance, neighbor))

    return distances, previous

def shortest_path_to(adjacency, start, end):
    distances, previous = dijkstra(adjacency, start)
    path = []
    current = end
    while previous[current] is not None:
        path.insert(0, current)
        current = previous[current]
    path.insert(0, start)
    return path, distances[end]

P = int(input())
places = {input().strip() for _ in range(P)}

Q = int(input())
graph = {place: {} for place in places}
for _ in range(Q):
    src, dest, dist = input().split()
    dist = int(dist)
    graph[src][dest] = dist
    graph[dest][src] = dist

R = int(input())
requests = [input().split() for _ in range(R)]
for start, end in requests:
    if start == end:
        print(start)
        continue

    path, total_dist = shortest_path_to(graph, start, end)
    output = ""
    for i in range(len(path) - 1):
        output += f"{path[i]}->({graph[path[i]][path[i+1]]})->"
    output += f"{end}"
    print(output)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![5ae674fbb9931e77c4741633838ff5f](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\5ae674fbb9931e77c4741633838ff5f.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

题目略有难度，恶补两天数算做的我头晕眼花，pot在输出格式上也能卡好久。Dijkstra还是有些不足的，需要题解和ai的帮忙



