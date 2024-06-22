# Assignment #4: 排序、栈、队列和树

Updated 0005 GMT+8 March 11, 2024

2024 spring, Complied by ==崔灏梵 生命科学学院==



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:

Learn about Time complexities, learn the basics of individual Data Structures, learn the basics of Algorithms, and practice Problems.

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：Windows 11(c)

Python编程环境：Spyder IDE 5.2.2, PyCharm 2023.1.4 (Professional Edition)

C/C++编程环境：Mac terminal vi (version 9.0.1424), g++/gcc (Apple clang version 14.0.3, clang-1403.0.22.14.1)



## 1. 题目

### 05902: 双端队列

http://cs101.openjudge.cn/practice/05902/



思路：



代码

```python
# class queue():
    def __init__(self):
        self.items=[]

    def size(self):
        return len(self.items)

    def adeque(self):
        self.items.pop()

    def bdeque(self):
        self.items=self.items[1:]

    def inque(self,x):
        self.items.append(x)

    def pre(self):
        if len(self.items)>0:
            return ' '.join(map(str,self.items))
        else:
            return 'NULL'

t=int(input())
for i in range(t):
    n=int(input())
    q=queue()
    for i in range(n):
        a,b=map(int,input().split())
        if a==1:
            q.inque(b)
        elif a==2:
            if b==0:
                q.bdeque()
            elif b==1:
                q.adeque()
    print(q.pre())

```



代码运行截图 ==（至少包含有"Accepted"）==

![c6638d46f1c3136ddfa709e9f1bd4f8](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\c6638d46f1c3136ddfa709e9f1bd4f8.png)



### 02694: 波兰表达式

http://cs101.openjudge.cn/practice/02694/



思路：



代码

```python
# def isn(x):
    try:
        float(x)
        return True
    except Exception as e:
        return False

def gan(a,b,c):
    if a=='+':
        return float(b)+float(c)
    elif a=='-':
        return float(b)-float(c)
    elif a=='*':
        return float(b)*float(c)
    elif a=='/':
        return float(b)/float(c)

h=input().split()
i=0
while len(h)>3 and i<len(h):
    if isn(h[i]) and isn(h[i+1]):
        h=h[:i-1]+[gan(h[i-1],h[i],h[i+1])]+h[i+2:]
        i-=2
    else:
        i+=1
x=gan(h[0],h[1],h[2])
print('%.6f'%x)

```



代码运行截图 ==（至少包含有"Accepted"）==

![1a54722792bf072c65f6ff736b39467](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\1a54722792bf072c65f6ff736b39467.png)



### 24591: 中序表达式转后序表达式

http://cs101.openjudge.cn/practice/24591/



思路：



代码

```python
# def infix_to_postfix(expression):
    precedence = {'+':1, '-':1, '*':2, '/':2}
    stack = []
    postfix = []
    number = ''

    for char in expression:
        if char.isnumeric() or char == '.':
            number += char
        else:
            if number:
                num = float(number)
                postfix.append(int(num) if num.is_integer() else num)
                number = ''
            if char in '+-*/':
                while stack and stack[-1] in '+-*/' and precedence[char] <= precedence[stack[-1]]:
                    postfix.append(stack.pop())
                stack.append(char)
            elif char == '(':
                stack.append(char)
            elif char == ')':
                while stack and stack[-1] != '(':
                    postfix.append(stack.pop())
                stack.pop()

    if number:
        num = float(number)
        postfix.append(int(num) if num.is_integer() else num)

    while stack:
        postfix.append(stack.pop())

    return ' '.join(str(x) for x in postfix)

n = int(input())
for _ in range(n):
    expression = input()
    print(infix_to_postfix(expression))

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![3182ae198a83572b44fef8316382041](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\3182ae198a83572b44fef8316382041.png)



### 22068: 合法出栈序列

http://cs101.openjudge.cn/practice/22068/



思路：



代码

```python
# def jud(s1,s2):
    if len(s1)!=len(s2):
        return 'NO'
    else:
        stack=[]
        i=0
        for j in s1:
            stack.append(j)
            while stack and stack[-1]==s2[i]:
                i+=1
                stack.pop()
        if stack:
            return 'NO'
        else:
            return 'YES'

s1=input()
while True:
    try:
        s2=input()
        print(jud(s1,s2))
    except BaseException:
        break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![bb650e0ca819c621cf508dca05ec594](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\bb650e0ca819c621cf508dca05ec594.png)



### 06646: 二叉树的深度

http://cs101.openjudge.cn/practice/06646/



思路：



代码

```python
# class TreeNode():
    def __init__(self, val, left, right):
        self.val = val
        self.left = left
        self.right = right

def get_depth(nodes, index):
    if index == -1:
        return 0
    left_depth = get_depth(nodes, nodes[index].left)
    right_depth = get_depth(nodes, nodes[index].right)
    return max(left_depth, right_depth) + 1

n = int(input())
nodes = {}
for i in range(1, n+1):
    left, right = map(int, input().split())
    nodes[i] = TreeNode(i, left, right)
depth = get_depth(nodes, 1)
print(depth)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![b384064be09dbd55f27c6e0c73e75c4](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\b384064be09dbd55f27c6e0c73e75c4.png)



### 02299: Ultra-QuickSort

http://cs101.openjudge.cn/practice/02299/



思路：



代码

```python
# def merge_sort(lst):
    if len(lst) <= 1:
        return lst, 0

    middle = len(lst) // 2
    left, inv_left = merge_sort(lst[:middle])
    right, inv_right = merge_sort(lst[middle:])

    merged, inv_merge = merge(left, right)

    return merged, inv_left + inv_right + inv_merge

def merge(left, right):
    merged = []
    inv_count = 0
    i = j = 0

    while i < len(left) and j < len(right):
        if left[i] <= right[j]:
            merged.append(left[i])
            i += 1
        else:
            merged.append(right[j])
            j += 1
            inv_count += len(left) - i 
    merged += left[i:]
    merged += right[j:]

    return merged, inv_count

while True:
    n = int(input())
    if n == 0:
        break

    lst = []
    for _ in range(n):
        lst.append(int(input()))

    _, inversions = merge_sort(lst)
    print(inversions)

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![46aee0c631572d7d60e95ecefdd1175](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\46aee0c631572d7d60e95ecefdd1175.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

对树的理解还不够深入，需要再加强练习

快排算法与具体题目的结合



