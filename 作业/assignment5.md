# Assignment #5: "树"算：概念、表示、解析、遍历

Updated 2124 GMT+8 March 17, 2024

2024 spring, Complied by ==崔灏梵 生命科学学院==



**说明：**

1）The complete process to learn DSA from scratch can be broken into 4 parts:

Learn about Time complexities, learn the basics of individual Data Structures, learn the basics of Algorithms, and practice Problems.

2）请把每个题目解题思路（可选），源码Python, 或者C++（已经在Codeforces/Openjudge上AC），截图（包含Accepted），填写到下面作业模版中（推荐使用 typora https://typoraio.cn ，或者用word）。AC 或者没有AC，都请标上每个题目大致花费时间。

3）提交时候先提交pdf文件，再把md或者doc文件上传到右侧“作业评论”。Canvas需要有同学清晰头像、提交文件有pdf、"作业评论"区有上传的md或者doc附件。

4）如果不能在截止前提交作业，请写明原因。



**编程环境**

==（请改为同学的操作系统、编程环境等）==

操作系统：macOS Ventura 13.4.1 (c)

Python编程环境：Spyder IDE 5.2.2, PyCharm 2023.1.4 (Professional Edition)

C/C++编程环境：Mac terminal vi (version 9.0.1424), g++/gcc (Apple clang version 14.0.3, clang-1403.0.22.14.1)



## 1. 题目

### 27638: 求二叉树的高度和叶子数目

http://cs101.openjudge.cn/practice/27638/



思路：



代码

```python
# class TreeNode():
    def __init__(self, val, left, right):
        self.val = val
        self.left = left
        self.right = right

def get_leaves(nodes):
    s=0
    for i in nodes:
        if i.left == -1 and i.right == -1:
            s+=1
    return s

def get_root(nodes):
    root=nodes[0].val
    for i in nodes:
        if i.left==root or i.right==root:
            root=i.val
    return root

def get_depth(nodes,index):
    if index == -1:
        return -1
    left_depth = get_depth(nodes, nodes[index].left)
    right_depth = get_depth(nodes, nodes[index].right)
    return max(left_depth, right_depth) + 1

n = int(input())
nodes = []
for i in range(n):
    left, right = map(int, input().split())
    nodes.append(TreeNode(i, left, right))
s=str(get_depth(nodes,get_root(nodes)))+' '+str(get_leaves(nodes))
print(s)

```



代码运行截图 ==（至少包含有"Accepted"）==

![7d1981215d69556c7a817e914bd903d](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\7d1981215d69556c7a817e914bd903d.png)



### 24729: 括号嵌套树

http://cs101.openjudge.cn/practice/24729/



思路：



代码

```python
# class TreeNode:
    def __init__(self, val):
        self.val = val
        self.children = []

def parse_tree(s):
    stack = []
    node = None
    for char in s:
        if char.isalpha():
            node = TreeNode(char)
            if stack:
                stack[-1].children.append(node)
        elif char == '(':
            if node:
                stack.append(node)
                node = None
        elif char == ')':
            if stack:
                node = stack.pop()
    return node


def preorder(node):
    output = [node.val]
    for child in node.children:
        output.extend(preorder(child))
    return ''.join(output)

def postorder(node):
    output = []
    for child in node.children:
        output.extend(postorder(child))
    output.append(node.val)
    return ''.join(output)

s = input().strip()
s = ''.join(s.split())
root = parse_tree(s)
if root:
    print(preorder(root))
    print(postorder(root))

```



代码运行截图 ==（至少包含有"Accepted"）==

![eee0c3ccc56b41935a9c040253a48c6](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\eee0c3ccc56b41935a9c040253a48c6.png)



### 02775: 文件结构“图”

http://cs101.openjudge.cn/practice/02775/



思路：



代码

```python
# 
class Node:
    def __init__(self,name):
        self.name=name
        self.dirs=[]
        self.files=[]

def print_(root,m):
    pre='|     '*m
    print(pre+root.name)
    for Dir in root.dirs:
        print_(Dir,m+1)
    for file in sorted(root.files):
        print(pre+file)
        
tests,test=[],[]
while True:
    s=input()
    if s=='#':
        break
    elif s=='*':
        tests.append(test)
        test=[]
    else:
        test.append(s)
for n,test in enumerate(tests,1):
    root=Node('ROOT')
    stack=[root]
    print(f'DATA SET {n}:')
    for i in test:
        if i[0]=='d':
            Dir=Node(i)
            stack[-1].dirs.append(Dir)
            stack.append(Dir)
        elif i[0]=='f':
            stack[-1].files.append(i)
        else:
            stack.pop()
    print_(root,0)
    print()
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![9a693f7abac9fb91c83a1fda94e3f73](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\9a693f7abac9fb91c83a1fda94e3f73.png)



### 25140: 根据后序表达式建立队列表达式

http://cs101.openjudge.cn/practice/25140/



思路：



代码

```python
# class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def build_tree(postfix):
    stack = []
    for char in postfix:
        node = TreeNode(char)
        if char.isupper():
            node.right = stack.pop()
            node.left = stack.pop()
        stack.append(node)
    return stack[0]

def level(root):
    queue = [root]
    traversal = []
    while queue:
        node = queue.pop(0)
        traversal.append(node.value)
        if node.left:
            queue.append(node.left)
        if node.right:
            queue.append(node.right)
    return traversal

n = int(input().strip())
for _ in range(n):
    postfix = input().strip()
    root = build_tree(postfix)
    e = level(root)[::-1]
    print(''.join(e))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![1456429532888877e5f830a1d37ea52](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\1456429532888877e5f830a1d37ea52.png)



### 24750: 根据二叉树中后序序列建树

http://cs101.openjudge.cn/practice/24750/



思路：



代码

```python
# def build_tree(inorder, postorder):
    if not inorder or not postorder:
        return []

    root_val = postorder[-1]
    root_index = inorder.index(root_val)

    left_inorder = inorder[:root_index]
    right_inorder = inorder[root_index + 1:]

    left_postorder = postorder[:len(left_inorder)]
    right_postorder = postorder[len(left_inorder):-1]

    root = [root_val]
    root.extend(build_tree(left_inorder, left_postorder))
    root.extend(build_tree(right_inorder, right_postorder))

    return root

def main():
    inorder = input().strip()
    postorder = input().strip()
    preorder = build_tree(inorder, postorder)
    print(''.join(preorder))


if __name__ == "__main__":
    main()

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![cf99c97fa1d306c89f190de3d7e29aa](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\cf99c97fa1d306c89f190de3d7e29aa.png)



### 22158: 根据二叉树前中序序列建树

http://cs101.openjudge.cn/practice/22158/



思路：



代码

```python
# class TreeNode:
    def __init__(self, value):
        self.value = value
        self.left = None
        self.right = None

def build_tree(preorder, inorder):
    if not preorder or not inorder:
        return None
    root_value = preorder[0]
    root = TreeNode(root_value)
    root_index_inorder = inorder.index(root_value)
    root.left = build_tree(preorder[1:1+root_index_inorder], inorder[:root_index_inorder])
    root.right = build_tree(preorder[1+root_index_inorder:], inorder[root_index_inorder+1:])
    return root

def postorder_traversal(root):
    if root is None:
        return ''
    return postorder_traversal(root.left) + postorder_traversal(root.right) + root.value

while True:
    try:
        preorder = input().strip()
        inorder = input().strip()
        root = build_tree(preorder, inorder)
        print(postorder_traversal(root))
    except EOFError:
        break

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![f3db65c0227c83f0eaedeefc46bd075](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\f3db65c0227c83f0eaedeefc46bd075.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

作业较为吃力，还是对树的具体实现理解不够，还需要多看大佬们的代码好好参悟![3FE56401](C:\Users\ADMINI~1\AppData\Local\Temp\SGPicFaceTpBq\25612\3FE56401.png)



