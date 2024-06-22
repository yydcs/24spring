# Assignment #7: April 月考

Updated 1557 GMT+8 Apr 3, 2024

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

### 27706: 逐词倒放

http://cs101.openjudge.cn/practice/27706/



思路：



代码

```python
# h=list(input().split())
h.reverse()
print(' '.join(h))

```



代码运行截图 ==（至少包含有"Accepted"）==

![e94a2e4afc5158ef12f122f1ec6e61e](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\e94a2e4afc5158ef12f122f1ec6e61e.png)



### 27951: 机器翻译

http://cs101.openjudge.cn/practice/27951/



思路：



代码

```python
# 

```



代码运行截图 ==（至少包含有"Accepted"）==

![2b03be29d3de08bb674c67a7d3a6c49](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\2b03be29d3de08bb674c67a7d3a6c49.png)



### 27932: Less or Equal

http://cs101.openjudge.cn/practice/27932/



思路：



代码

```python
# 

```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![cffc92921c690ce41886696d9dbaeec](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\cffc92921c690ce41886696d9dbaeec.png)



### 27948: FBI树

http://cs101.openjudge.cn/practice/27948/



思路：



代码

```python
# 
def construct_FBI_tree(s):
    if '0' in s and '1' in s:
        node='F'
    elif '1' in s:
        node='I'
    else:
        node='B'
    if len(s)>1:
        mid =len(s)//2
        left =construct_FBI_tree(s[:mid])
        right =construct_FBI_tree(s[mid:])
        return left+right+node
    else: 
        return node
n=int(input())
s=input()
print(construct_FBI_tree(s))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![429483a07908b79f1998ef493cb3d9f](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\429483a07908b79f1998ef493cb3d9f.png)



### 27925: 小组队列

http://cs101.openjudge.cn/practice/27925/



思路：



代码

```python
# 
t=int(input())
te=[]
for i in range(t):
    group=list(input().split())
    te.append(group)
bic=[]
dic=[]
while True:
    dis=input()
    if dis=='STOP':
        break
    elif len(dis.split())>1:
        dus=0
        a,b=dis.split()
        for i in range(t):
            if b in te[i]:
                dus=i
                break
        if dus in bic:
            s=bic.index(dus)
            dic[s].append(b)
        else:
            bic.append(dus)
            dic.append([b])
    elif dis=='DEQUEUE':
        while not dic[0]:
            dic.pop(0)
            bic.pop(0)
        print(dic[0].pop(0))
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![c0fb582096b2f54138c5cd9f2d6749f](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\c0fb582096b2f54138c5cd9f2d6749f.png)



### 27928: 遍历树

http://cs101.openjudge.cn/practice/27928/



思路：



代码

```python
# 
def order(dic,root):
    pis=dic[root]+[root]
    pis.sort()
    for i in pis:
        if i !=root:
            order(dic,i)
        else:
            print(root)

n=int(input())
dic= {}
for i in range(n):
    nums=list(map(int,input().split()))
    dic[nums[0]]=nums[1:]
root=0
for i in dic.keys():
    mis=True
    for j in dic.keys():
        if i in dic[j]:
            mis=False
            break
    if mis:
        root=i
        break
order(dic,root)
```



代码运行截图 ==（AC代码截图，至少包含有"Accepted"）==

![00c89711f8641181e4af2b85514d762](D:\Backup\Documents\WeChat Files\wxid_yezm06l8sr5g12\FileStorage\Temp\00c89711f8641181e4af2b85514d762.png)



## 2. 学习总结和收获

==如果作业题目简单，有否额外练习题目，比如：OJ“2024spring每日选做”、CF、LeetCode、洛谷等网站题目。==

这次题目意外简单（还是计概适合我），2小时大概是AC5，递归有点小小绕进去了，看来还要多练



