# 模版

**leetcode上数组构建树的测试用例**

定义树结构
```
# Definition for a binary tree node.
class TreeNode:
    def __init__(self, x):
        self.val = x
        self.left = None
        self.right = None
```
列表创建二叉树
```
def Create_tree(root,llist,i):
    #创建过程也是从根开始a，创左子树b，再创b的左子树，如果b的左子树为空，返回none。
    #再接着创建b的右子树，
    if i<len(llist):
        if llist[i] ==None: return None
        else:
            root=TreeNode(llist[i])
            #往左递推
            root.left=Create_tree(root.left,llist,2*i+1)#从根开始一直到最左，直至为空，
            #往右回溯
            root.right=Create_tree(root.right, llist,2*i+2)#再返回上一个根，回溯右，
            #再返回根'
            return root  #这里的return很重要
    return root
```
迭代
```
from typing import List
class Solution:
    def inorderTraversal(self, root):
        res = []
        def helper(root):
            if not root: return None
            helper(root.left)
            res.append(root.val)
            helper(root.right)
        helper(root)
        return res    
```
递归
```
# 中序打印二叉树（非递归）
    def inOrderTraverse2(self,root):
        res = []
        stack = []
        # 用p当做指针
        p = root
        while p or stack:
            # 把左子树压入栈中
            while p:
                stack.append(p)
                p = p.left
            # 输出 栈顶元素
            p = stack.pop()
            res.append(p.val)
            # 看右子树
            p = p.right
        return res
```

测试代码
```
if __name__=="__main__":
    s = Solution()
    root = ['1','2','3',None,'4','5']
    root = Create_tree(None,root,0)
    r = s.inorderTraversal(root)
    print(r)
```