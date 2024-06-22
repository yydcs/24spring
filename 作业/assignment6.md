# Assignment #6: "树"算：Huffman,BinHeap,BST,AVL,DisjointSet

Updated 2214 GMT+8 March 24, 2024

2024 spring, Complied by ==崔灏梵 生命科学学院==



**说明：**

1）这次作业内容不简单，耗时长的话直接参考题解。

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：macOS Ventura 13.4.1 (c)

Python编程环境：Spyder IDE 5.2.2, PyCharm 2023.1.4 (Professional Edition)

C/C++编程环境：Mac terminal vi (version 9.0.1424), g++/gcc (Apple clang version 14.0.3, clang-1403.0.22.14.1)



## 1. 题目

### 22275: 二叉搜索树的遍历

http://cs101.openjudge.cn/practice/22275/



思路：



代码

```python
# 
class Treenode:
    def __init__(self,val):
        self.val=val
        self.left=None
        self.right=None

class Tree:
    def __init__(self,node):
        self.root=node

def build_tree(nodes):
    if not nodes:
        return None
    a=len(nodes)
    for i in range(1,len(nodes)):
        if nodes[i]>nodes[0]:
            a=i
            break
    node=Treenode(nodes[0])
    node.left=build_tree(nodes[1:a])
    node.right=build_tree(nodes[a:])
    return node

def postorder(node):
    output=[]
    if node:
        if node.left:
            output.extend(postorder(node.left))
        if node.right:
            output.extend(postorder(node.right))
        output.append(node.val)
    return output

n=int(input())
nodes=list(map(int,input().split()))
t=postorder(build_tree(nodes))
print(' '.join(map(str,t)))
```



代码运行截图 ==（至少包含有"Accepted"）==

![7fbce076dea56ee06f14416093008ae](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\7fbce076dea56ee06f14416093008ae.png)



### 05455: 二叉搜索树的层次遍历

http://cs101.openjudge.cn/practice/05455/



思路：



代码

```python
# class Treenode:
    def __init__(self,val):
        self.val=val
        self.left=None
        self.right=None
    def pre(self):
        q=[self]
        output=[]
        while q:
            if q[0].left:
                q.append(q[0].left)
            if q[0].right:
                q.append(q[0].right)
            output.append(q.pop(0).val)
        return ' '.join(map(str,output))
    def add(self,node):
        cur=self
        while True:
            if node.val>cur.val:
                if cur.right:
                    cur=cur.right
                else:
                    cur.right=node
                    break
            else:
                if cur.left:
                    cur=cur.left
                else:
                    cur.left=node
                    break


i=1
inf=list(map(int,input().split()))
num=[inf[0]]
nodes=Treenode(inf[0])
while i < len(inf):
    if inf[i] in num:
        pass
    else:
        num.append(inf[i])
        nodes.add(Treenode(inf[i]))
    i+=1
print(nodes.pre())

```



代码运行截图 ==（至少包含有"Accepted"）==



![be81ecf16610302ebe3878b2872a9a5](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\be81ecf16610302ebe3878b2872a9a5.png)

### 04078: 实现堆结构

http://cs101.openjudge.cn/practice/04078/

练习自己写个BinHeap。当然机考时候，如果遇到这样题目，直接import heapq。手搓栈、队列、堆、AVL等，考试前需要搓个遍。



思路：



代码

```python
# class BinHeapq:
    def __init__(self):
        self.heapList=[0]
        self.currentSize=0

    def add(self,x):
        self.heapList.append(x)
        self.currentSize+=1
        i=self.currentSize
        while i//2>0:
            if self.heapList[i]<self.heapList[i // 2]:
                self.heapList[i],self.heapList[i // 2]=self.heapList[i // 2],self.heapList[i]
            i=i//2
    def percDown(self, i):
        while (i * 2) <= self.currentSize:
            mc = self.minChild(i)
            if self.heapList[i] > self.heapList[mc]:
                tmp = self.heapList[i]
                self.heapList[i] = self.heapList[mc]
                self.heapList[mc] = tmp
            i = mc

    def minChild(self, i):
        if i * 2 + 1 > self.currentSize:
            return i * 2
        else:
            if self.heapList[i * 2] < self.heapList[i * 2 + 1]:
                return i * 2
            else:
                return i * 2 + 1
    def delMin(self):
        retval = self.heapList[1]
        self.heapList[1] = self.heapList[self.currentSize]
        self.currentSize = self.currentSize - 1
        self.heapList.pop()
        self.percDown(1)
        return retval
h=BinHeapq()
for i in range(int(input())):
    op=list(map(int,input().split()))
    if op[0]==1:
        h.add(op[1])
    elif op[0]==2:
        print(h.delMin())

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==



![6cb063d5a994b9727279c5b13f1cc78](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\6cb063d5a994b9727279c5b13f1cc78.png)

### 22161: 哈夫曼编码树

http://cs101.openjudge.cn/practice/22161/



思路：



代码

```python
# 
import heapq
class Node:
    def __init__(self, weight, char=None):
        self.weight = weight
        self.char = char
        self.left = None
        self.right = None

    def __lt__(self, other):
        if self.weight == other.weight:
            return self.char < other.char
        return self.weight < other.weight

def build_huffman_tree(characters):
    heap = []
    for char, weight in characters.items():
        heapq.heappush(heap, Node(weight, char))

    while len(heap) > 1:
        left = heapq.heappop(heap)
        right = heapq.heappop(heap)
        merged = Node(left.weight + right.weight, min(left.char, right.char))
        merged.left = left
        merged.right = right
        heapq.heappush(heap, merged)

    return heap[0]

def encode_huffman_tree(root):
    codes = {}

    def traverse(node, code):
        if node.left is None and node.right is None:
            codes[node.char] = code
        else:
            traverse(node.left, code + '0')
            traverse(node.right, code + '1')

    traverse(root, '')
    return codes

def huffman_encoding(codes, string):
    encoded = ''
    for char in string:
        encoded += codes[char]
    return encoded

def huffman_decoding(root, encoded_string):
    decoded = ''
    node = root
    for bit in encoded_string:
        if bit == '0':
            node = node.left
        else:
            node = node.right

        if node.left is None and node.right is None:
            decoded += node.char
            node = root
    return decoded
n = int(input())
characters = {}
for _ in range(n):
    char, weight = input().split()
    characters[char] = int(weight)

huffman_tree = build_huffman_tree(characters)
codes = encode_huffman_tree(huffman_tree)

strings = []
while True:
    try:
        line = input()
        strings.append(line)
    except EOFError:
        break

results = []
for string in strings:
    if string[0] in ('0','1'):
        results.append(huffman_decoding(huffman_tree, string))
    else:
        results.append(huffman_encoding(codes, string))

for result in results:
    print(result)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![ec82182b134143aa2b8031c78ccbcfd](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\ec82182b134143aa2b8031c78ccbcfd.png)



### 晴问9.5: 平衡二叉树的建立

https://sunnywhy.com/sfbj/9/5/359



思路：



代码

```python
# 
class Node:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None
        self.height = 1

class AVL:
    def __init__(self):
        self.root = None

    def insert(self, value):
        if not self.root:
            self.root = Node(value)
        else:
            self.root = self._insert(value, self.root)

    def _insert(self, value, node):
        if not node:
            return Node(value)
        elif value < node.value:
            node.left = self._insert(value, node.left)
        else:
            node.right = self._insert(value, node.right)

        node.height = 1 + max(self._get_height(node.left), self._get_height(node.right))

        balance = self._get_balance(node)

        if balance > 1:
            if value < node.left.value:	# 树形是 LL
                return self._rotate_right(node)
            else:	# 树形是 LR
                node.left = self._rotate_left(node.left)
                return self._rotate_right(node)

        if balance < -1:
            if value > node.right.value:	# 树形是 RR
                return self._rotate_left(node)
            else:	# 树形是 RL
                node.right = self._rotate_right(node.right)
                return self._rotate_left(node)

        return node

    def _get_height(self, node):
        if not node:
            return 0
        return node.height

    def _get_balance(self, node):
        if not node:
            return 0
        return self._get_height(node.left) - self._get_height(node.right)

    def _rotate_left(self, z):
        y = z.right
        T2 = y.left
        y.left = z
        z.right = T2
        z.height = 1 + max(self._get_height(z.left), self._get_height(z.right))
        y.height = 1 + max(self._get_height(y.left), self._get_height(y.right))
        return y

    def _rotate_right(self, y):
        x = y.left
        T2 = x.right
        x.right = y
        y.left = T2
        y.height = 1 + max(self._get_height(y.left), self._get_height(y.right))
        x.height = 1 + max(self._get_height(x.left), self._get_height(x.right))
        return x

    def preorder(self):
        return self._preorder(self.root)

    def _preorder(self, node):
        if not node:
            return []
        return [node.value] + self._preorder(node.left) + self._preorder(node.right)

n = int(input().strip())
sequence = list(map(int, input().strip().split()))

avl = AVL()
for value in sequence:
    avl.insert(value)

print(' '.join(map(str, avl.preorder())))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![74fb9eaca0eb3f1f560bf448f8f9af2](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\74fb9eaca0eb3f1f560bf448f8f9af2.png)



### 02524: 宗教信仰

http://cs101.openjudge.cn/practice/02524/



思路：



代码

```python
# class UnionFind:
    def __init__(self, n):
        self.parent = list(range(n))
        self.size = [1] * n

    def find(self, x):
        if self.parent[x] != x:
            self.parent[x] = self.find(self.parent[x])
        return self.parent[x]

    def union(self, x, y):
        root_x = self.find(x)
        root_y = self.find(y)
        if root_x != root_y:
            if self.size[root_x] < self.size[root_y]:
                root_x, root_y = root_y, root_x
            self.parent[root_y] = root_x
            self.size[root_x] += self.size[root_y]

def count_religions(n,edges):
    uf = UnionFind(n)
    for i, j in edges:
        uf.union(i - 1, j - 1)
    roots = set()
    for i in range(n):
        roots.add(uf.find(i))
    return len(roots)

k = 1
while True:
    n, m = map(int, input().split())
    if n == 0 and m == 0:
        break
    edges = []
    for _ in range(m):
        i, j = map(int, input().split())
        edges.append((i, j))
    num_religions = count_religions(n,edges)
    print(f"Case {k}: {num_religions}")
    k += 1

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![e1937889bba41af73d644a5c45624f9](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\e1937889bba41af73d644a5c45624f9.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

作业好难，部分题目还是需要靠题解和GPT，基本每道题都耗时比较长



